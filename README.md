Web Sentinel – Phishing Detection Chrome Extension
=================================================

Web Sentinel is a lightweight Chrome extension that analyzes the current page using 16 heuristics and a simple linear classifier to flag potential phishing pages. It runs silently and only alerts when a threat is detected.

Features
--------
- Heuristic scanner with 16 signals (URL structure, mixed domains, forms, iframes, etc.)
- Linear model producing phishing (1) or legitimate (-1) output
- Silent auto-scan on page load with an in-page warning banner on detection
- Manual scan from popup
- Reputable-root allowlist to reduce false positives on CDN-heavy sites (only neutralizes cross-domain features)

Install (Unpacked)
------------------
1. Open Chrome → Extensions (chrome://extensions)
2. Enable Developer mode
3. Click “Load unpacked” and select this folder (`Web Sentinel`)

Usage
-----
- Navigate to any normal https page
- Click the extension icon → “Manual Scan” to see the verdict in the popup
- Auto-scan runs on page load and shows a top banner only when phishing is detected

Permissions
-----------
- `tabs`, `activeTab`, `scripting` – needed to query active tab and inject/execute the content scanner when not already present
- `host_permissions: <all_urls>` – scanner runs on all sites to protect users across the web

How Detection Works
-------------------
The content script computes a 16-element feature vector with values in {-1, 0, 1} and applies a fixed-weight linear model. See MODEL.md for details.

Allowlist
---------
To avoid false positives on reputable, CDN-heavy sites (e.g., google.com, microsoft.com), the extension neutralizes only the three cross-domain ratio features on those roots. All other features remain active.

Privacy
-------
- No browsing data is sent to external servers
- All analysis happens locally on the page

Development
-----------
- Manifest V3 (`manifest.json`)
- Content script: `content.js` (scanner and model)
- Popup UI: `popup.html`, `popup.js`

Roadmap
-------
- Optional user-managed allowlist in the popup
- Telemetry-free local logs toggle (for debugging only)
- Additional heuristics and model improvements

License
-------
MIT – see LICENSE


