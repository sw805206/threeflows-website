# Scope

Refer to SCOPE.md as the source of truth.

| | |
|---|---|
| **Project type** | multi-html-page website |
| **Purpose** | Introduce Threeflows Solutions LLC, a boutique consulting firm that focuses on helping small business owners to launch and scale their e-commerce business. It provides related education, consultation, and ongoing management. |
| **Output** | www.threeflows.com |
| **Apps & Locations** | Hosting — GitHub Pages<br>Domain, Nameserver, DNS — Cloudflare<br>Admin — Google Workspace<br><br>Cloudflare: https://dash.cloudflare.com/e772d948b5a11f47e94732bb489b5b71/threeflows.com<br>GitHub: https://github.com/sw805206/threeflows-website<br>Local: /Users/swai/sw805206/threeflows-website |
| **Git disciplines** | Deploys from main. |
| **Gov documents** | CLAUDE.md (copy from MOTHERSHIP; Part A also in Claude setting)<br>SCOPE.md<br>STYLE.md and STYLE.css<br>ARCHITECTURE.md<br><br>All live in repo, copy to Claude project. Refer to the repo version as source of truth. |
| **Out of scope** | No formal database — Google Sheet serves as interim backend (see ARCHITECTURE.md).<br><br>Login/auth — not supported short term; long-term solution TBD.<br><br>Forms submit to Google Apps Script endpoints (generic no-DB pattern). The script code is owner-managed and not in this repo. Detail lives in ARCHITECTURE.md.<br><br>Hard constraints: static, vanilla JS, no frameworks, lean dependencies. |
