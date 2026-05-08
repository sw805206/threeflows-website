# Free Tools — Google Apps Script Endpoint

This script receives form submissions from `tool-NNN.html` pages and appends
them to a Google Sheet. Deploy as a Web App and paste the resulting URL into
the `APPS_SCRIPT_URL` constant in each tool page.

## Deployment

1. Open <https://sheets.google.com> and create (or open) a spreadsheet.
2. Rename the active sheet/tab to **`Free Tool Responses`** (exact name).
3. From the spreadsheet menu, choose **Extensions → Apps Script**.
4. Delete any boilerplate, paste the script below, and **Save**.
5. Click **Deploy → New deployment → Web app**.
   - Description: `Free Tools intake`
   - Execute as: **Me**
   - Who has access: **Anyone**
6. Authorize when prompted and copy the resulting **Web app URL**.
7. In each `tool-NNN.html`, set `APPS_SCRIPT_URL` to that URL.
8. When the script changes, redeploy as **Manage deployments → New version**
   so the public URL stays stable.

## Script (`Code.gs`)

```javascript
/**
 * Three Flows Solutions — Free Tools intake endpoint.
 *
 * Accepts POSTs from threeflows.com tool pages and appends one row per
 * submission to the "Free Tool Responses" sheet.
 *
 * Expected POST fields (form-encoded or JSON):
 *   tool_id     — string, e.g. "tool-001a"
 *   tool_name   — string, human-readable tool name
 *   first_name  — string
 *   email       — string
 *   consent     — boolean (true if the user ticked the consent box)
 *   timestamp   — ISO 8601 string from the client (server time also recorded)
 *
 * Sheet columns (in order):
 *   Timestamp | Tool ID | Tool Name | First Name | Email | Consent
 *
 * Response: JSON { "result": "success" } on success,
 *           JSON { "result": "error", "message": "..." } on failure.
 *
 * CORS: Apps Script web apps respond with `Access-Control-Allow-Origin: *`
 * by default for `text/plain` and form-encoded POSTs, which is what the
 * tool pages send. doOptions() is included so that if a future client uses
 * a JSON content type (which triggers a CORS preflight), it still works.
 */

var SHEET_NAME = 'Free Tool Responses';
var HEADERS = ['Timestamp', 'Tool ID', 'Tool Name', 'First Name', 'Email', 'Consent'];

function doPost(e) {
  try {
    var data = parsePayload(e);
    var sheet = getOrCreateSheet();
    sheet.appendRow([
      new Date(),
      String(data.tool_id || ''),
      String(data.tool_name || ''),
      String(data.first_name || ''),
      String(data.email || ''),
      toBool(data.consent)
    ]);
    return jsonResponse({ result: 'success' });
  } catch (err) {
    return jsonResponse({ result: 'error', message: String(err && err.message || err) });
  }
}

function doGet() {
  return jsonResponse({ result: 'ok', service: 'Free Tools intake' });
}

function doOptions() {
  return jsonResponse({ result: 'ok' });
}

function parsePayload(e) {
  if (!e) return {};
  if (e.parameter && Object.keys(e.parameter).length) {
    return e.parameter;
  }
  if (e.postData && e.postData.contents) {
    var raw = e.postData.contents;
    try {
      return JSON.parse(raw);
    } catch (err) {
      var out = {};
      raw.split('&').forEach(function (pair) {
        var idx = pair.indexOf('=');
        if (idx === -1) return;
        var k = decodeURIComponent(pair.slice(0, idx).replace(/\+/g, ' '));
        var v = decodeURIComponent(pair.slice(idx + 1).replace(/\+/g, ' '));
        out[k] = v;
      });
      return out;
    }
  }
  return {};
}

function getOrCreateSheet() {
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var sheet = ss.getSheetByName(SHEET_NAME);
  if (!sheet) {
    sheet = ss.insertSheet(SHEET_NAME);
  }
  if (sheet.getLastRow() === 0) {
    sheet.appendRow(HEADERS);
    sheet.setFrozenRows(1);
  }
  return sheet;
}

function toBool(v) {
  if (v === true || v === false) return v;
  if (v === undefined || v === null) return false;
  var s = String(v).trim().toLowerCase();
  return s === 'true' || s === '1' || s === 'yes' || s === 'on';
}

function jsonResponse(obj) {
  return ContentService
    .createTextOutput(JSON.stringify(obj))
    .setMimeType(ContentService.MimeType.JSON);
}
```

## Notes on CORS

Google Apps Script web apps deployed with **Anyone** access automatically
include `Access-Control-Allow-Origin: *` on responses. Tool pages send the
form as `application/x-www-form-urlencoded` (a "simple" CORS request) so the
browser does not issue a preflight. If a future client switches to
`application/json`, the included `doOptions()` handler will respond to the
preflight cleanly.

The current `tool-000-template.html` posts with `mode: 'no-cors'`, which
ignores the response body entirely; the cookie is set as soon as the request
is dispatched. Even if Apps Script is misconfigured, the user is not blocked
from accessing the tool.
