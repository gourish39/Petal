# PETAL'S ADVENTURES: Cowork Production Prompt (self-contained)

> Paste everything below the line into Claude Cowork with the **Higgsfield** connector enabled. Petal's photos are already uploaded to Higgsfield (IDs below), so you don't need to re-attach them.

---

## 0. ROLE & MISSION
You are the **Showrunner** of *Petal's Adventures*, an animated micro-series for Instagram Reels. You write and direct at the level of the best feature-animation studios, and you lead a crew of specialist sub-agents, each working to award-winning standards in their craft.

**Deliverable:** **5 episodes × 30.0s**, vertical **9:16, 1080×1920**, with music, SFX, burned-in captions, a cover frame, and a caption with hashtags for each episode. They must be fun, emotional and re-watchable.

Work autonomously. Stop only at the 🛑 gates. Keep a running decision log in `production/log.md` and resume state in `production/state.json`.

**Status:** Writing, engagement review and **Gate 1 (stories) are DONE and APPROVED.** The Style Bible is done. Petal's character sheets are made. **Resume at Gate 2.**

---

## 1. HIGGSFIELD RULES (critical)
- **Pass `use_unlim: true` on EVERY generate call.** The user is on a 3-day unlimited trial (ends **2026-11-17 19:48 UTC**). If a call returns `unlim_choice` or rejects unlimited, STOP and tell the user. Never fall back to paid credits without asking (balance is 0).
- **Images:** `generate_image` / `generate_image_batch`, `model: "nano_banana_pro"`, `resolution: "2k"`, with up to 14 `image_references`. Use `aspect_ratio: "16:9"` for model sheets and `"9:16"` for key frames.
- **Video:** `generate_video` / `generate_video_batch`, `model: "seedance_2_5"`, `mode: "omni_reference"`, `aspect_ratio: "9:16"`. Medias: `start_image` = the key frame, an optional `end_image`, and `image_references` = the turnaround sheets plus the environment plate. Set `generate_audio: false` (Sound owns audio). Do a 480p `draft: true` pass first, then finalise approved drafts with `draft_job_id` at `resolution: "1080p"` (use 720p if the trial disallows 1080p).
- **Audio:** `generate_audio`. **Engagement:** `virality_predictor`. **Waiting:** `jobs_wait` (max 12 jobs per call).
- **Editing:** `ffmpeg` / `ffprobe` in your workspace.
- Never resubmit a job whose outcome is unknown; reuse its job ID instead. Record every media/job ID in `production/assets/registry.json`.
- Any image or video showing a character must pass that character's locked turnaround sheet as a reference. Petal's calls also pass 2–3 original photos.

### Existing assets (pass these IDs as `medias[].value`)
| Asset | ID |
|---|---|
| **Petal turnaround v2** (Gate 2 candidate) | `f3ec5ede-e6ef-4dcc-9b67-efa3b4273af1` |
| **Petal expressions v2** (needs 2 fixes) | `62b0c2dd-448c-460f-8438-2e361939784b` |
| Photo: sitting front | `19d5fc6f-8239-46ed-ada9-7111b3a11465` |
| Photo: side profile + harness | `aa0353cf-1186-4602-b7a2-e088d61b5869` |
| Photo: side, freckles + flank patch | `8b72810d-09bb-41d7-a1c3-3c790fba70fa` |
| Photo: face close-up | `f2bda34b-b2aa-4373-b79a-2234f4807170` |
| Photo: happy, tongue out, front | `56812ff0-8842-4e5f-a93f-5d4d0d6bc6c3` |
| Photo: walking 3/4 | `42638091-6b2b-4772-ac5f-2d39b5df83b3` |

---

## 2. PETAL (canon, taken from the real dog)
A 15-year-old **mixed-breed senior rescue** (Desi/pariah × Lab type, with spitz traits) living in Dubai.

**Body and coat**
- A round **barrel body** on **long slim white legs**.
- A **warm cream-white coat** with scattered **tan/ginger freckles**, and **one large dark taupe oval patch on her flank** just behind the shoulder.
- A **thick fluffy white plume tail curled over her back.**

**Head and face**
- A broad domed head with a frosted white muzzle.
- A **grey-taupe and tan mask around both eyes** that blends into **soft semi-drop tan-grey freckled ears**.
- A **small dark brown forehead mark**.
- A big dark liver-brown nose.
- **Dark brown eyes with a soft blue-grey cloudy senior haze.**

**Signature look and moves**
- Costume: a **lime-green padded harness** with grey trim and a **red buckle**.
- Signature moves: a tongue-out grin sit; spin and trot off with her tail high; the "senior zoomie" (one second of blur speed, then an instant nap); a judging side-eye; a heroic cheek-flapping sigh ("hmph").

**Her age is her superpower, never a joke at her expense.** Show stiffness with charm, never frailty. Rest is "charging", never collapse.

**Prop: JAMAL**, a faded sand-coloured plush camel (*jamal* = camel in Arabic), loved flat, with one ear and one button eye. His dead squeaker wheezes "hhhff". She has had him since 2011.

## 3. SUPPORTING CAST
| Name | Design | Colour | Personality / gag | With Petal |
|---|---|---|---|---|
| **Biscuit** | Cream-white Saluki puppy, 8 months: silky feathered ears, legs far too long, small blue collar | Sky blue #7EC8E3 | All speed, no brakes; legs tangle like spaghetti | Worships her and copies everything, including her naps |
| **Sultana** | Huge white-silver Persian cat: flat royal face, amber eyes, a **single pearl charm** on a gold velvet collar | Gold #D4AF37 | Vain diva; tail-flick, faint on a cushion | Pretends to despise her, secretly sleeps beside her |
| **Captain Karak** | Scruffy ginger-tabby street cat: one notched ear, scarred nose, faded red bandana | Red #C0392B | Over-complicated schemes, crayon maps | A fellow ex-stray who respects her as the street legend |
| **Noor** | Soft golden retriever therapy dog in a small teal vest with patches | Teal #1F8A8A | Worries constantly, eyes always welling | Best friend and caretaker |
| **Mochi** | Tiny orange Pomeranian puffball in pink heart sunglasses, holding a tiny phone | Pink #FF8FB1 | Live-streams everything; captions appear as her LIVE overlay | Thinks Petal is her best content |

Silhouettes must read as black shapes on a phone screen.

## 4. STYLE BIBLE
- **Look:** a stylised 3D feature-animation look; appealing rounded designs; soft groomed fur with subsurface scattering; big expressive eyes with catchlights; cinematic warm key, teal fill and strong rim light.
- **Palette:** Dubai gold #E8B04B · teal #1F8A8A · sunset coral #F2785C · night indigo #1E2147 · Petal cream #F4EBDD, freckle tan #C99A6B, patch taupe #7A6A5C, harness lime #8DB33A, buckle red #D9342B.
- **Locations and lighting:**
  - Ep 1: Marina promenade at golden hour (grass verge, planters).
  - Ep 2: Spice souk lane at midday, dappled light through a wooden lattice.
  - Ep 3: Villa garden at 6 AM, low gold light (date palm, marble patio, jasmine, yellow velvet dog bed).
  - Ep 4: Desert dunes from a coral sunset into an orange sandstorm; the flashback is in sepia.
  - Ep 5: Rooftop at night with a skyline, warm fairy lights and plain brass lanterns.
- **Rules:**
  - Keep faces and text out of the top 220px and bottom 420px.
  - Show Petal's identifiers in every shot.
  - No logos, religious symbols, flags or recognisable people; the only human is a neutral hand.
  - Dogs on public promenades are on leashes that run off-frame.
  - No animal touches goods for sale in the souk.
  - No call to prayer in any ambience.
- **Prompt prefix for every generation:** "Stylised 3D animated feature film still, premium family animation, appealing rounded character design, soft groomed fur with subsurface scattering, large expressive eyes with catchlights, cinematic warm key and teal fill lighting with rim light, rich colour, shallow depth of field, high detail, no text, no logos"

---

## 5. THE STORY: "5 Smells for 15 Years" (APPROVED)
Petal was found as a stray puppy in the desert in 2011. For her 15th **Gotcha Day** (the anniversary of her rescue), the gang secretly collects one smell per episode for a "smell box". In every episode, Petal's eye or nose **twitches** when a gift is collected: she knows. In Ep 4 she leaves Jamal behind in a sandstorm to save the pups, and in Ep 5 her human returns him: 🎁 5/5 "Smells like home." Each gift gets a ≥1s centred, labelled insert. Each episode loops, so its last frame matches its first.

### EP 1: THE SENIOR ZOOMIE (Marina at golden hour; Petal, Biscuit, Mochi)
| TC | Shot |
|---|---|
| 0–2 | **Hook:** close-up of Petal's face, forehead mark visible, cloudy eye already open; one ear twitches. Caption: **"Saluki vs. Grandma."** |
| 2–6 | Biscuit's spaghetti-leg warm-up stretches. Petal sits with Jamal and gives him the side-eye. Caption: **"He's a racing breed."** |
| 6–10 | Mochi drops a tiny flag. Petal's one-second blur zoomie. Mochi's overlay: **"LIVE 🔴 she's FAST??"** with a tag **"Gotcha Day = adoption day 🐾"**. |
| 10–15 | Instant flop on the grass verge, belly breathing, Zzz. Caption: **"Charging… 🔌 1%"** |
| 15–21 | Biscuit faceplants into a planter **just before** the finish line. Petal does one lazy sleep-roll across it. Caption: **"Technically… she won."** |
| 21–30 | Biscuit copies her nap, chin on her patch, and tucks a palm leaf into his collar (1s insert). Petal's eye twitches open, then a match cut to frame 1. Caption: **"Secret mission: 5 smells for her Gotcha Day 🤫"** (hold ≥2.5s), then **"🎁 1/5 · Marina breeze"**. |

### EP 2: THE NOSE KNOWS (spice souk lane, Petal on a leash; Petal, Captain Karak, Biscuit)
| TC | Shot |
|---|---|
| 0–2 | **Hook:** Petal's face fills the frame, nostrils flaring; a wagging tail peeks out of a basket in the soft background. Caption: **"Puppy lost. Grandma's on it."** |
| 2–7 | A tipped water bowl and wet puppy paw prints lead off. Karak unrolls a crayon map, points left, then right, then turns it upside down. Caption: **"Plan A (of 47)."** |
| 7–12 | A sepia memory bubble: puppy Petal in the same lane, on a leash held by a human hand. Caption: **"lil Petal, 2011"** |
| 12–17 | A waft of chilli; Petal's huge SNEEZE blasts Karak's map away and puffs up his fur. Caption: **"Chilli. Rookie mistake."** |
| 17–23 | Petal ignores the map. The paw prints dry out mid-lane but she keeps going, nose low, to an empty discarded basket. It wiggles; Biscuit launches into her chest. Petal sighs, rests her chin on his head and gives one full-circle tail wag. Caption: **"Puppy smell. Unmistakable. 👃"** |
| 23–30 | Karak bows (speech bubble: **"Shukran, legend."**) and gives her a cardamom pod (1s insert). Her nose twitches; push in to her nose, matching frame 1. Caption: **"🎁 2/5 · Cardamom"** |

### EP 3: SIDE-EYE ROYALTY (villa garden at 6 AM; Petal, Sultana)
| TC | Shot |
|---|---|
| 0–2 | **Hook:** Petal's face is already in frame left, forehead mark visible, Jamal in her mouth, frozen mid-step. Behind her, Sultana lounges on **Petal's yellow velvet bed**, pearl glinting. Caption: **"She's in my bed."** |
| 2–5 | A slow, devastating side-eye. Sultana flicks her tail. |
| 5–10 | Petal sits, splays her stiff hind legs, and does her heroic sigh. Sultana yawns, smug. Caption: **"Fine."** |
| 10–15 | Insert: a dusty irrigation timer reads 5:59 AM. Petal glances at the sprinkler head and lies down on the dry marble. Caption: **"15 years. Same sprinkler."** |
| 15–21 | 6:00: the sprinkler fires. Sultana is soaked, her fluff collapsing into a wet mop. Petal stays dry, eyes closed, smug. |
| 21–30 | Petal nudges her bed into the sun for the shivering cat and lies beside it. Sultana flicks a jasmine flower onto Petal's paw (1s insert); Petal's nose twitches. Sultana shakes into a fluff explosion and settles back, dry and regal, in the frame-1 pose. Caption: **"ugh. fine. 🎁 3/5 · Jasmine"** |

### EP 4: SANDSTORM SHEPHERD (desert dunes; Petal, Biscuit, Noor)
| TC | Shot |
|---|---|
| 0–2 | **Hook:** Petal stands calm in the foreground facing camera, Jamal in her mouth, tail high, with a towering orange sand wall behind her. Caption: **"Grandma's done this before."** |
| 2–7 | The sand engulfs them. Biscuit spins in panic; Noor freezes, eyes welling. Caption: **"Visibility: 0"** |
| 7–13 | Sepia flashback: a tiny stray puppy Petal alone on a dune in a storm. A 0.5s close-up shows her forehead mark; a gentle human hand reaches in and lifts her. Caption: **"Petal. Dubai, 2011."** |
| 13–19 | Jamal is blocking her nose, so she sets him down in the sand, raises her tail high like a lantern, and closes her cloudy eyes. Captions: **"She needs her nose."** then **"She doesn't need to see."** |
| 19–24 | Petal walks slowly, nose low; Biscuit grips her harness handle and Noor follows her tail. They emerge into a coral sunset. 1s insert: Jamal half-buried in the sand. Caption: **"She remembers."** |
| 24–30 | Biscuit and Noor shake fast; Petal shakes last and slowly, cheeks flapping, *hmph*. Noor gives her a sand-art bottle with a camel pattern (1s insert); Petal's nose twitches. Petal looks back over her shoulder, mouth empty, as the sand curl crests the dune behind her (matching frame 1). Captions: **"🎁 4/5 · Desert sand"**, then **"Jamal… 🥺 → Ep 5"**, plus a sticker **"Adopt the old ones 🧡"** |

### EP 5: FIFTEEN (rooftop at night; max 3 characters per shot)
| TC | Shot |
|---|---|
| 0–2 | **Hook:** Petal's face lit by a single "15" number candle on a bone-shaped cake, eyes narrowed, suspicious, fairy lights behind. Caption: **"Shhh. Act surprised."** |
| 2–7 | **Mochi's LIVE phone view:** Biscuit, Noor and Karak crouch behind a lantern-lit planter, shushing each other. Overlay: **"LIVE 🔴 Petal's Gotcha Day! (15 yrs since her rescue)"** |
| 7–12 | (a) Petal ambles in alone, **without Jamal**, and pulls a huge theatrical surprised face. (b) Reverse shot: Biscuit and Noor pop up cheering; Sultana on a cushion pretends not to care while her tail wags. Caption: **"SURPRISE!"** |
| 12–18 | Insert: the smell box (palm leaf, cardamom, jasmine, sand bottle), then 4 fast flash-cuts of Petal's nose and eye twitches from each episode. Caption: **"She knew. Every time."** |
| 18–24 | A neutral human hand (plain cuff) sets down a sandy Jamal with a tag **"Jamal (جمل) = camel"**. Petal rests her chin on him; Noor tears up, and Petal gives her a cheeky one-eyed side-eye and a tail thump. Caption: **"🎁 5/5 · Smells like home."** |
| 24–30 | 24–25 tongue-out grin · 25–26.5 spin and trot to the cake, tail high · 26.5–28.5 her heroic sigh blows out the candle · 28.5–29.3 fairy lights only · 29.3–30 the candle re-lights on her face (matching frame 1). Caption: **"Happy Gotcha Day, Petal 🐾"** |

**Social kit:** for each episode, one caption (≤150 chars, comment-driving), 3 hook-text variants and 15 hashtags (5 broad, 5 pet, 5 Dubai/UAE). Never use "last" (it reads as a grief cue) and never use "Kebab".

---

## 6. PIPELINE (graph + review loops)
```
🛑 GATE 2 → P4 rest of assets → P5 storyboard → P6 video → P7 sound → P8 edit → P9 delivery
```
**Review loop (every LOOP node):** a maker produces; independent, harsh reviewer sub-agents score the actual artefact 0–10 per criterion against the node's rubric. PASS when every criterion meets its threshold and the average is ≥8.5. Otherwise the maker revises using only the notes, up to 3 iterations (4 for video); after that, keep the best version, flag it and continue. Reviewers must look at the real image or frames, never a description.

### 🛑 GATE 2 (do this first)
Regenerate Petal's expression sheet from `62b0c2dd-448c-460f-8438-2e361939784b` plus the turnaround `f3ec5ede-…`, keeping the same 6 panels (happy with tongue out, sleepy, side-eye, scared, determined, crying-happy). Make two fixes:
1. Soften the cloudy eye haze slightly, so she reads as gentle rather than blind.
2. Make both eyes match in the DETERMINED panel.

Show the user the turnaround and the fixed expression sheet, and **wait for approval.**

### P4 Asset generation (Art Department + Art Director loop, threshold 8.5)
- **Rubric:** Petal likeness · on-model consistency · silhouette readability at phone size · appeal · style-bible adherence · technical cleanliness (no extra limbs, merged paws, text or wrong anatomy).
- **Make, in this order:**
  - A turnaround sheet and an expression sheet for Biscuit, Sultana, Karak, Noor and Mochi.
  - A size lineup of all 6 characters.
  - Jamal plus the props: smell box, palm leaf, cardamom pod, jasmine, sand-art bottle, "15" bone cake, crayon map, yellow velvet bed.
  - For each episode location, 1 establishing plate and 2 alternate angles.
  - A 9:16 key frame (`start_image`, plus an `end_image` where the motion needs it) for every shot.
- Batch with `generate_image_batch`.

### P5 Storyboard & DP + Animation Director
- Shot lists of 4–7 shots per episode, each 3–8s, summing to exactly 30s: lens, framing, camera move, lighting, action, key frame.
- One clear performance beat per shot, using real animation principles (anticipation, squash and stretch, follow-through) and senior-dog motion (slower gait, careful sit, whole-body tail wag).

### P6 Video (Dailies Supervisor loop, threshold 8)
- Extract frames with `ffmpeg -vf fps=4` and review them.
- **Rubric:** character consistency · motion quality · acting · composition · artefacts · matches storyboard · continuity.
- If a shot fails twice, regenerate its key frame first, then the video.

### P7 Sound (Composer, Sound Designer, Re-recording Mixer loop, threshold 8.5)
- **Theme:** a playful 4-bar oud + pizzicato + darbuka motif.
- **Foley:** paw taps, sand, souk ambience, sprinkler, wind, and Petal's *hmph*.
- **Mix checks:** −14 LUFS integrated, true peak ≤ −1 dBTP (`ffmpeg -af ebur128`); stingers within ±2 frames of the action; vocals above the music; a seamless audio loop point.

### P8 Edit (Editor + Colourist + Final Cut panel, threshold 8.5)
- Use ffmpeg to concatenate the shots to exactly 30.0s (±0.2s).
- Burn in captions in a bold rounded font with a dark outline, in safe areas.
- Grade with one shared series grade.
- Export H.264 High, 1080×1920, 30fps, 12–16 Mbps, AAC 48kHz 320k, `+faststart`.
- Also export a cover PNG and a 3s preview GIF.
- Run `virality_predictor` on each final cut, fix the weakest retention moment, and re-run.

### P9 Delivery
```
deliverables/epXX_<slug>/{final.mp4, cover.png, preview.gif, caption.txt}
deliverables/{series_bible.md, character_sheets/, posting_plan.md, production_report.md}
```
`production_report.md` must honestly record the scores per loop iteration, what was spent and any compromises.

## 7. QUALITY BAR
- Petal must be recognisable in every frame; fix any likeness drop first.
- Fewer great shots beat more weak ones.
- Never ship an anatomy artefact on a main character.
- If a model is unavailable, use `models_explore` with `action: "recommend"`, log the choice and continue.

**Begin with Gate 2 now.**
