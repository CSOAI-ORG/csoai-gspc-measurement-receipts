# csoai-gspc-measurement-receipts

By Nicholas Templeman, CSOAI Ltd (UK Companies House 16939677)

URL: https://councilof.ai

# A 22-Axis AI Measurement Board in 7 Lines of curl

The CSOAI board lives at `councilof.ai/board`. It shows every measurement we've issued. The whole thing — including signature verification — fits in a single HTTP request:

```bash
curl -s https://councilof.ai/api/gspc | jq '.cards | length'
```

That tells you how many signed cards exist. Want to verify one?

```bash
curl -s https://councilof.ai/api/gspc/sha256/<hash> | jq '{axis, methodology, measurement, signature}'
```

Want to check the signature?

```bash
curl -s https://councilof.ai/api/gspc/sha256/<hash>/verify
```

The board has **22 axes** measured across transparency, safety, fairness, accountability, robustness, privacy, and 16 more. The latest cards, the historical cards, the methodology, and the cryptography — all public, all signed, all queryable.

No login. No paywall. No "contact sales for an enterprise demo."

This is what governance looks like when the artifact is the receipt, not the certificate.

---

**Nicholas Templeman**, CSOAI Ltd (UK 16939677).

---

## About CSOAI

CSOAI (Council of AI) is the UK's sovereign AI governance measurement body.
Live board: https://councilof.ai/board
22 axes measured, signed, verifiable.
