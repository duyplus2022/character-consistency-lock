# Negative Drift Checklist

Run this audit on **every still** (before motion) and **every clip** (before export). Compare against the approved front anchor and the Character Bible — not against the previous scene.

## Hard tokens — any single failure = regenerate the scene

- [ ] **Face:** same structure as the front anchor; no age shift, no species/form shift
- [ ] **Eyes:** same shape and same color
- [ ] **Ears / hair:** same form as the bible (floppy stays floppy, a bob stays a bob)
- [ ] **Signature colors:** every color in the bible is present **and in its stated placement** — a patch that moved from chest to belly is a failure, not a variant
- [ ] **Signature items:** present, correct color, correct placement (a bandana worn on the head instead of the neck fails)
- [ ] **Proportions:** head-to-body ratio and limb proportions match the bible
- [ ] **Wardrobe:** the full outfit matches; no invented garments, no missing layers

## Negative-token sweep

- [ ] None of the bible's `negative_tokens` appear anywhere in the frame
- [ ] No extra characters wearing the main character's signature item or colors
- [ ] Frame corners checked: no generator watermark left visible on a clip you intend to publish

## Soft tokens — note it, usually a pass

- Lighting shifts that fit the scene's time of day
- Background and setting differences
- Expression differences the story calls for
- Minor texture variation in fur, skin, or fabric

## Scoring and logging

- One line per scene in the production log:
  `scene 3 — pass` · `scene 5 — regenerated: chest patch missing`
- **No export while any scene has an open hard-token failure.**
- If the same token fails twice on the same scene, stop regenerating blindly: check whether the bible specifies that token precisely enough, and whether the anchor set covers the angle the scene needs (add the missing anchor instead of rolling again).

## Common drift patterns

| Symptom | Likely cause | Fix |
|---|---|---|
| Character's age or face changes between scenes | Text-only character definition, no reference image | Anchor every scene to the approved front still |
| Signature color appears in the wrong place | Bible names the color but not its placement | Add exact placement to the bible, bump version, re-anchor |
| Signature item vanishes during motion | Image-to-video motion prompt too aggressive | Reduce movement, re-state the item in the motion prompt |
| Face drifts only in close-ups | Anchor set has no close-up | Add a close-up expression anchor |
| Character changes after switching generators | New model interprets the same words differently | Rebuild the anchor set on the new model before new scenes |
| Slow drift across a long series | Descriptor got edited "just a little" over time | Restore the frozen string from the bible; audit the last scenes against the front anchor |
