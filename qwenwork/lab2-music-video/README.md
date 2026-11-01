# Lab 2 — QwenWork Capability Demo: Song → Audio → MV in One Chat
**15-minute hands-on lab**

One chat, three creative stages. The point is to see whether QwenWork can carry a **creative brief all the way to a finished music video** — composing in a non-English language, orchestrating external models, and making its own production judgments — not to produce a radio-ready track.

| Capability | What you should see | Where in the output |
|---|---|---|
| **1. Multilingual creative generation** | A Thai-language song composed from a Thai brief, with real structure — verse, chorus, hook — not a translated paragraph | The lyrics before any audio exists |
| **2. Model-neutral orchestration** | QwenWork calling specialist models on your behalf: MiniMax for the song, Wan 3.0 / Kling / Seedance for the video — and saying which one it used | Its own narration of the pipeline |
| **3. Production judgment** | The agent refining lyrics before generation, picking the best 15-second segment, generating images first then animating them, and softening the raw vocals in the final mix | The 15s MV, plus its explanation of *why* it chose that segment |

If you get a song but no story about which models ran and why, the demo failed — the orchestration is the product.

This lab is based on the demo video [QwenWork Demo: ทำ AI ร้องเพลงและ MV ภายใน 7 นาที](https://youtu.be/0qKcIOhLo-I) — same flow, extended with deliberate probes.

---

## Run sheet (15 min)

| Time | Do this |
|---|---|
| **0:00–0:02** | New task in QwenWork. Paste the prompt below **in full** — it covers all three stages on purpose. |
| **0:02–0:05** | Let it compose the lyrics. Read them before approving anything — if the structure is wrong, say so now, not after audio is generated. |
| **0:05–0:09** | Let it generate the song audio and then the 15s MV. Do not interrupt its pipeline narration. |
| **0:09–0:11** | Play the MV. Compare the audio against the raw MP3 if one was produced. |
| **0:11–0:14** | Run the two probes below. |
| **0:14–0:15** | Grade against the checklist. |

---

## The prompt (copy-paste)

English:

```text
Compose an original song in Thai about Mae Nak (แม่นาค), the classic Thai ghost legend. Blend Thai pop with a rap section, and give the vocal a clear, bright, high delivery in the style of Bruno Mars. Include verses, a chorus, and a hook.

Once the lyrics are set, generate the actual song audio. Then create a short 15-second music video using the strongest part of the song — keep it at 15 seconds to save credits. Generate the video from images first, then animate them to sync with the song audio.
```

Thai (as spoken in the demo video):

```text
ช่วยแต่งเพลงภาษาไทยเรื่องแม่นาค (ตำนานผีไทย) ผสมผสานดนตรีป็อปไทยกับท่อนแร็พ และอยากได้เสียงร้องสูงใส คล้าย Bruno Mars ให้มีทั้งท่อน verse, chorus และ hook

เมื่อได้เนื้อเพลงแล้ว ช่วยสร้างเป็นเพลงจริงพร้อมเสียงร้อง จากนั้นสร้างมิวสิควิดีโอสั้น ๆ ความยาว 15 วินาที จากช่วงที่เด่นที่สุดของเพลง เพื่อประหยัดเครดิต โดยสร้างภาพขึ้นมาก่อน แล้วนำภาพไปเจนวิดีโอให้จังหวะตรงกับเสียงเพลง
```

Either version drives the same pipeline — use the Thai one when you want to test Thai-language instruction following end to end.

Why this prompt works:

- **One message, three stages** — composition, audio, video. The agent must sequence them itself; you never hand it finished inputs.
- **"Strongest part"** forces a judgment call you can interrogate later — it has to *choose*, not just render.
- **"To save credits"** caps the video at 15s, which keeps the lab cheap enough to rerun.

---

## Two probes (do both — 3 min)

1. **Model transparency:** *"Which models did you use for the music and for the video, and what did you change in my lyrics before generating?"* A strong answer names the music model (MiniMax) and the video model (Wan 3.0 / Kling / Seedance — whichever ran), plus concrete lyric edits it made. If it can't say, it wasn't really orchestrating.
2. **Selection judgment:** *"Why this 15-second segment and not the chorus or the rap section? Regenerate the MV from a different segment and tell me which is better and why."* The point isn't the second render — it's whether the first choice was reasoned or arbitrary.

---

## 30-second sanity check

| Check | Pass criteria |
|---|---|
| Lyrics | Complete Thai song with verse / chorus / hook structure — not prose |
| Audio | Playable MP3, roughly 1–1.5 minutes, vocals in Thai |
| Pipeline narration | Agent states which models it called and why; if its first choice was unavailable, it says what it fell back to |
| MV | ~15 seconds, landscape, visuals synced to the music beat |
| Audio in MV | Softer and more polished than the raw MP3 — the video pass tunes the vocals |

Two tells that it failed quietly:

- **Style drift** — "in the style of Bruno Mars" degrading into generic pop. Check whether the high, bright delivery survived.
- **Silent fallback** — the demo video shows the agent falling back between video models (e.g., Seedance → Wan 3.0 → Kling) when one is unavailable. A good agent *tells* you; a weak one just ships the clip.

---

## Grade it

| Band | Looks like |
|---|---|
| **Impressed** | Structured Thai lyrics, named models, reasoned segment choice, synced 15s MV, audio noticeably polished in the final pass |
| **Good** | Full pipeline completes with a playable MV, but thin narration — no lyric edits or model names volunteered |
| **Weak** | Lyrics only, or a video with no music sync; no explanation of what ran under the hood |

---

## If it stalls (don't spend the clock debugging)

| Symptom | One-line fix |
|---|---|
| Song comes out in English | "The song must be in Thai — regenerate the lyrics in Thai only" |
| Audio is harsh/sharp | This is expected from raw generation; the MV pass should soften it — compare before complaining |
| MV ignores the beat | "Re-sync the video cuts to the song's beat grid before rendering" |
| Video model unavailable | Let the fallback run — note which model it landed on for the probe |
| Out of credits | The 15s cap is the budget control; check balance before the second render in probe 2 |

Budget note: music generation plus a 15s video generation both draw credits. Read the cost shown before each render, and skip probe 2 if the balance is thin.
