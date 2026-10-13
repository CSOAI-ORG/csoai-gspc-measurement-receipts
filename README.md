# csoai-gspc-measurement-receipts

By Nicholas Templeman, CSOAI Ltd (UK Companies House 16939677)

URL: https://councilof.ai

# The Council of AI measurement board in four curl commands

The board is public and signed. You can read it, and check a signed card, without an account. Every command below was run against the live site on 13 October 2026. The counts are not typed here on purpose: the board states its own, so read them live.

**1. What the board says about itself**

```bash
curl -s https://councilof.ai/api/gspc | jq -r '.totals.public_count, .totals.separation_public_count'
```

Read the two lines together. The first counts axes with a run behind them. The second says on how many of the model-comparison axes one model was separated from the rest; a tie is reported as a tie.

**2. The axes, with their state and sample size**

```bash
curl -s https://councilof.ai/api/gspc | jq -r '.axes[] | "\(.axis)\t\(.status)\tn=\(.n)"'
```

**3. Take one signed card and ask the verifier about it**

```bash
CARD=$(curl -s https://councilof.ai/signed/card_index.json | jq -r '.cards[0].card_url')
curl -s "https://councilof.ai$CARD" \
  | curl -s -X POST https://councilof.ai/api/verify -H 'content-type: application/json' --data-binary @- \
  | jq '{state, reason, rule}'
```

`state` says whether the card's body reproduces its own id and its signature verifies under a published key. `rule` links the steps to repeat the check yourself, offline.

**4. The published Merkle root**

```bash
curl -s https://councilof.ai/api/root | jq '{as_of, card_count, merkle_root}'
```

The signed card index (command 3) and the public root (command 4) are separate sets of cards. Their counts differ, and they are not meant to be added together.

No login. No paywall. Verification is free.

This is what governance looks like when the artifact is the receipt, not the certificate. We measure; we do not certify. A result that was not measured is reported as unmeasured.

---

**Nicholas Templeman**, CSOAI Ltd (UK 16939677).

---

## About CSOAI

CSOAI (Council of AI) is an independent AI measurement body.
Live board: https://councilof.ai
Corrections record: https://councilof.ai/api/corrections

_Corrected 13 October 2026. The earlier text said 22 axes, named axes the board does not have, and gave two commands that did not work (`.cards` on `/api/gspc`, and `/api/gspc/sha256/<hash>`)._
