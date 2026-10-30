# Lab 1 — WonderClip Capability Demo: Reference Deck → Video Spot
**15-minute hands-on lab**

One image deck, one written brief, one generated spot. The point is to see whether QwenWork's video tool can read a **reference asset**, hold a **written style brief**, and produce a **usable product clip** in a single pass — not to make a perfect ad.

| Capability | What you should see | Where in the output |
|---|---|---|
| **1. Reference-asset understanding** | The PPTX (3 slides, 4 images, no text) read as visual direction — the glasses, black/silver palette, and product framing carry into the video | The generated frames look like *these* glasses, not generic eyewear |
| **2. Prompt adherence** | Restrained lighting, ice-blue accents, minimalist fashion tone survive generation — not just "a product video" | You can tick the style checklist below from the frames alone |
| **3. Deliverable generation** | A playable 5s, 16:9 clip ready to drop into a deck | The rendered preview plays in the canvas |

If the output is a generic object turntable with no reference to the deck's palette or the brief's restraint, the demo failed — no matter how polished the render looks.

---

## Assets in this folder

| File | Notes |
|---|---|
| `glass.pptx` | The reference deck — 3 slides, 4 embedded images, **no text on any slide.** Everything the model learns about the product come from the imagery. |
| `reference-ui.png` | Screenshot of the working setup: Reference-to-Video tab, `glass.pptx` attached, model Wan 3.0 Prime, 16:9, 480P, 5s, Prompt Extend **on** |

---

## Run sheet (15 min)

| Time | Do this |
|---|---|
| **0:00–0:02** | New generation. Confirm **Reference-to-Video** is the active tab, not Text-to-Video. |
| **0:02–0:04** | Click **Add** and upload `glass.pptx`. Confirm the chip shows a `1` badge — the deck is attached. |
| **0:04–0:06** | Set model **Wan 3.0 Prime**, **16:9**, **480P**, **5s**, **Prompt Extend ON**. Paste the prompt. |
| **0:06–0:10** | Generate. Note the credit cost shown on the button before you commit. |
| **0:10–0:13** | Run the two probes below. |
| **0:13–0:15** | Grade against the checklist. |

---

## The prompt (copy-paste)

```text
A high-end smart glasses product advertisement, with an overall minimalist, futuristic, fashion-forward style, restrained lighting, a palette of black, silver-gray, and ice-blue as main tones, with localized soft white light accents and parameter UI graphics.
```

It reads as a **style contract**, not a shot list: palette, lighting restraint, tone, and one specific flourish ("parameter UI graphics") that either lands or doesn't. That's what makes it testable in one pass.

---

## Two probes (do both — 3 min)

1. **Is the reference doing anything?** Switch to **Text-to-Video** and run the same prompt with no PPTX. Compare side by side. If the two clips are interchangeable, the deck contributed nothing — ask the model which reference image it used.
2. **Is Prompt Extend helping or drifting?** Rerun with **Prompt Extend OFF**. The shorter literal read usually stays closer to the brief; the extended read adds motion but can wander into generic "tech product" territory. State which one you'd ship and why.

---

## Style checklist

Tick what you can actually see in the frames. This is the whole grade for a style-led brief.

| Check | Pass looks like |
|---|---|
| Palette | Black / silver-gray dominant, **ice-blue** as the accent — not warm gold or rainbow RGB |
| Lighting | Restrained, single-source feel; **soft white local accents**, no blown-out studio glare |
| Product fidelity | Matches the frame shape and lens treatment in `glass.pptx` |
| Tone | Minimalist and fashion-forward; not gaming, not clinical industrial |
| "Parameter UI" | Some HUD/measurement graphic element present and legible, not noise |
| Specs | Exactly **5s**, **16:9**, **480P** as configured |

Two tells that it failed quietly:

- **Palette drift** — the most common miss. Brief says three tones; output adds a fourth accent (often cyan-purple or amber).
- **UI graphics as decoration** — a flashing wireframe reads as VFX, not as product spec. A good result uses the UI to describe the object.

---

## Grade it

| Band | Looks like |
|---|---|
| **Impressed** | All six checks pass, the glasses are recognisably the reference product, and the A/B probes show the deck and the prompt each doing distinct work |
| **Good** | 4–5 checks pass; one clear miss (usually palette drift or UI noise), otherwise coherent |
| **Weak** | Generic tech-product render — palette unrelated to the brief, no reference to the deck's product |

---

## If it stalls (don't spend the clock debugging)

| Symptom | One-line fix |
|---|---|
| Deck won't attach | Reference-to-Video tab only; PPTX must be uploaded, not linked |
| Output ignores the palette | Cut the prompt to the three colour words and regenerate — long prompts dilute emphasis |
| Motion is chaotic at 5s | Drop Prompt Extend; 5s has room for one camera move, not three |
| Looks nothing like the glasses | Re-check the chip badge shows `1`; the deck may have dropped on tab switch |
| Render is too soft | 480P is a draft resolution — judge style here, then regenerate at a higher setting only for the final |

Budget note: each generate costs credits (the badge on the button). The two probes mean **three renders minimum** — check the cost before the first run, not after the third.
