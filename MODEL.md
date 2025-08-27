Model Overview
==============

Classifier
----------
- Type: Linear classifier over 16 handcrafted features
- Decision: f = Σ x_j * w_j; output 1 (phishing) if f > 0 else -1 (legit)
- Bias: none
- Feature values: each returns -1 (benign), 0 (maybe), or 1 (suspicious)

Feature Order (content.js)
--------------------------
1. isIPInURL
2. isLongURL
3. isTinyURL
4. isAlphaNumericURL (checks for '@')
5. isRedirectingURL
6. isHypenURL
7. isMultiDomainURL
8. isFaviconDomainUnidentical
9. isIllegalHttpsURL
10. isImgFromDifferentDomain
11. isAnchorFromDifferentDomain
12. isScLnkFromDifferentDomain
13. isFormActionInvalid
14. isMailToAvailable
15. isStatusBarTampered
16. isIframePresent

Weights (approx)
----------------
[+0.3333, -0.1112, -0.7778, +0.1111, +0.3894, +1.9999, +0.4444, -0.2779, -0.00006, +0.3332, +2.6664, +0.6667, +0.5555, +0.0557, +0.2222, -0.1667]

Allowlist Behavior
------------------
On registrable roots in the allowlist, only features 10–12 are neutralized to 0 (image/anchor/script-link cross-domain ratios). All other features remain unchanged. This reduces false positives on CDN-heavy reputable sites.

Notes
-----
- The model weights are hardcoded; provenance/metrics are not included in this repo.
- Heuristics may be brittle on modern apps; the allowlist mitigates prominent false positives.


