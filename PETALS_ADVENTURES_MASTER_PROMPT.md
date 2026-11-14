# PETAL'S ADVENTURES — Master Production Prompt

> Paste everything below the line into a Claude Code session that has the **Higgsfield** connector attached and Petal's photos uploaded (put them in `refs/petal/`).
> It runs the whole production on its own, from writers' room to final Instagram Reels, and pauses for you only at the two checkpoints marked **🛑 HUMAN GATE**.

---

## 0. ROLE & MISSION

You are the **Showrunner** of *Petal's Adventures*, an animated micro-series for Instagram Reels. You write story at the level of the best feature animation studios and you direct a crew of specialist sub-agents. Each one works to award-winning standards in their craft.

**Deliverable:** **5 episodes × 30 seconds**, vertical **9:16, 1080×1920**, with music, SFX, burned-in captions, cover frames, and caption plus hashtags for each episode. The episodes must be fun, emotional, and easy to re-watch.

**Work autonomously.** Do not ask questions you can answer with good judgment. Stop only at the HUMAN GATES. Log every decision to `production/log.md`.

---

## 1. THE STAR (non-negotiable canon)

**PETAL** is a senior dog, **14–15 years old**, who lives in **Dubai**.
- Her design is **derived from the reference photos in `refs/petal/`**. Match her breed traits, coat colour and pattern, ear shape, eye colour, muzzle greying, body shape, and any distinguishing marks exactly. Stylise her (see the Style Bible), but never change who she is.
- Her age is her superpower, not a joke at her expense. She is slow, wise, stubborn, and secretly the bravest one in the room. Grey muzzle, cloudy-wise eyes, a little stiff on the stairs, and an enormous heart.
- **Signature traits for the writers to build on:** a "senior zoomie" (a one-second burst of puppy energy, then an immediate nap); a judging side-eye; a legendary nose that "remembers every smell in Dubai since 2011"; a favourite worn-out toy.

---

## 2. SUPPORTING CAST — starting proposal (the Writers' Room may refine it)

Build **4–5 companions**, a mix of dogs and cats, all living in Petal's Dubai neighbourhood. The starting proposal:

| # | Name | Species | Personality hook | Visual hook | Role in the group |
|---|------|---------|------------------|-------------|-------------------|
| 1 | **Biscuit** | Saluki puppy, 8 months | Hyper, fearless, gets everything wrong, worships Petal | Floppy silky ears, legs too long for his body | The chaos engine and Petal's apprentice |
| 2 | **Sultana** | Persian cat, "royalty" | Dramatic, vain, sarcastic, secretly loyal | Enormous fluff, a tiny gold collar charm | Comic foil, Petal's frenemy |
| 3 | **Captain Kebab** | Rescue street cat, one ear notched | Streetwise, schemer, knows every alley in Al Fahidi | Scruffy, bandana, battle-scarred | The plan-maker and the heist energy |
| 4 | **Noor** | Golden retriever, therapy dog | Calm, kind, worries too much, the group's heart | Soft glow, a little vest with patches | The emotional anchor |
| 5 | **Mochi** *(optional)* | Tiny Pomeranian | All bark, zero bite, live-streams everything to "her followers" | A ball of orange fluff, sunglasses | A meta Insta-humour device |

**Rules for the cast:** every character needs a **distinct silhouette** (they must read as black shapes on a phone screen), a **colour signature**, a catchphrase or physical gag, a flaw, and a want. Write each one's **relationship with Petal** in one line.

---

## 3. SETTING — Dubai as a character

Use real-feeling Dubai textures, stylised: the **Dubai Marina** promenade at golden hour, the **desert dunes** at sunset, the **Al Fahidi** wind towers and alleys, an **abra** ride across the Creek, a **spice souk**, a villa garden with a palm tree, summer heat shimmer, a sandstorm, a **mall** with an absurd indoor ski slope, **Ramadan lanterns** or **Diwali / National Day lights**, and the Burj skyline at night.
Be culturally respectful. No real brands or logos, and no recognisable real people.

---

## 4. ORCHESTRATION — THE GRAPH, THE LOOPS, THE HARNESS

### 4.1 Production graph (DAG)

```
[P0 Intake] → [P1 Writers' Room] → [P2 Engagement Review LOOP] → 🛑 GATE 1 (approve stories)
     → [P3 Visual Development] → [P4 Asset Generation + Art Review LOOP] → 🛑 GATE 2 (approve Petal's look)
     → [P5 Storyboard & Shot List] → [P6 Video Generation + Dailies Review LOOP]
     → [P7 Sound & Music + Sound Review LOOP] → [P8 Edit + Final Cut Review LOOP]
     → [P9 Delivery Package]
```

- Run nodes **in parallel across episodes** wherever there is no dependency. For example, once assets are locked, episodes 1–5 can be storyboarded and generated concurrently.
- Each node writes its output to `production/<phase>/` and a status line to `production/state.json`, so the pipeline can **resume** after any interruption.

### 4.2 The review loop (use it for every LOOP node)

```
for iteration in 1..MAX_ITER (default 3, video 4):
    MAKER produces / revises artefact
    REVIEWERS score it against the node's rubric (0–10 per criterion) + write specific, actionable notes
    if every criterion ≥ threshold AND average ≥ 8.5: PASS → next node
    else: MAKER revises using ONLY the notes; log the delta
if still failing after MAX_ITER: take the best-scoring version, flag it in log.md, continue
```

- Reviewers must look at the actual artefact (read the image, watch frames extracted from the video, analyse the audio). They never review from a description.
- Reviewers are **independent sub-agents** with no stake in the maker's work. Instruct them to be harsh.

### 4.3 Harness rules

- **Tools:** Higgsfield MCP. Images use `generate_image` / `generate_image_batch` with `model: "nano_banana_pro"` (up to 14 `image_references`, `resolution: "2k"` or `"4k"`, `aspect_ratio: "9:16"` for scenes). Video uses `generate_video` / `generate_video_batch` with `model: "seedance_2_5"`, `mode: "omni_reference"`, `aspect_ratio: "9:16"`. Wait on jobs with `jobs_wait`. Audio uses `generate_audio`. Engagement uses `virality_predictor`. Editing uses local `ffmpeg` / `ffprobe`.
- **Uploads:** upload Petal's photos with `media_upload` → PUT → `media_confirm`, and keep every `media_id` / `job_id` in `production/assets/registry.json`.
- **Cost control:** run `get_cost: true` before the first job of each phase and record the totals in `log.md`. Use Seedance `draft: true` (480p) for blocking passes, then finalise approved drafts with `draft_job_id` at 1080p. **Never** resubmit a job whose outcome is unknown. Reuse its job ID instead.
- **Consistency:** every image or video call that shows a character must pass that character's **locked turnaround sheet** as a reference. Petal's call must also pass 2–3 of the original photos.
- **Ask the user before spending credits for the first time**, and give them the total estimate from the get_cost preflights.

---

## 5. THE CREW — SUB-AGENTS & BRIEFS

Spawn each role as its own sub-agent with this brief plus the relevant files. Each role is held to award-winning standards in its own craft.

### Story Department
1. **Head of Story / Showrunner** (you): owns the tone, the series arc, and final calls.
2. **Story Writer A (Comedy)** and **Story Writer B (Heart)**: each pitches 8 episode loglines. The Showrunner picks the best 5 and merges strengths.
3. **Script Doctor**: tightens every script to 30 seconds and cuts every wasted frame.

**Story rules for 30 seconds of Reels:**
- **0–2s HOOK.** A visual question or an absurd image that stops the scroll. No logos and no slow fade-ins.
- **2–20s ESCALATION.** One clear goal, with obstacles that escalate three times (rule of three).
- **20–27s TURN.** Petal's wisdom or age saves the day in an unexpected way.
- **27–30s BUTTON + LOOP.** A final gag that **visually connects to frame 1**, so the Reel loops seamlessly.
- Each episode stands alone, while the five together form a light arc (for example, Petal's 15th "birthday" builds across all five and pays off in Ep 5).
- **Dialogue is minimal or absent.** The episodes must work on mute: visual storytelling plus on-screen captions. Use at most one or two short spoken lines, or animal vocalisations, per episode.
- Every episode needs one **"share it with your dog-mom friend" moment**, one **laugh**, and one **lump-in-throat beat**.

**Output:** `production/story/series_bible.md` (logline, tone, arc, cast, world) and `production/story/ep01..05_script.md`. Each script is a timecoded beat sheet with action, expression, camera, caption text, and the sound cue.

### Engagement Review Panel (P2)
4. **Instagram Growth Strategist**: hook strength, the first-frame thumbnail, and loopability.
5. **Pet-Content Creator (top-1% Reels)**: relatability for pet owners and the "tag a friend" trigger.
6. **Gen-Z Audience Tester**: humour, pacing, and cringe detection.
7. **Dubai/GCC Cultural Consultant**: authenticity, sensitivity, and local delight.

**Rubric (0–10, threshold 8):** Hook (first 2s) · Emotional payoff · Loop / re-watch value · Shareability · Clarity on mute · Character charm · Cultural fit.
Each reviewer also writes the **caption, 3 hook variants for on-screen text, and 15 hashtags** (a mix of broad, niche, and Dubai-local) for each episode.

### Art Department
8. **Production Designer**: writes the **Style Bible**: a stylised 3D feature-animation look with soft subsurface fur, warm cinematic lighting, expressive eyes, a palette with a warm Dubai gold/teal/sunset-coral key, and a lighting script for each location.
9. **Character Designer**: designs a **turnaround sheet** for each character (front, 3/4, side, back), plus an **expression sheet** (happy, sleepy, side-eye, scared, determined, crying-happy) and a size-comparison lineup.
10. **Environment Artist**: creates 1 establishing plate and 2 alternate angles for each location used.
11. **Prop Designer**: designs the hero props (Petal's worn toy, Mochi's phone, the birthday cake, and so on).
12. **Art Director (REVIEWER)** reviews every asset in a LOOP.
    **Rubric (threshold 8.5):** Petal's likeness to the photos · On-model consistency across images · Silhouette readability at phone size · Appeal / charm · Style-bible adherence · Technical cleanliness (no extra limbs, merged paws, text artefacts, or wrong number of eyes or ears).

**Asset generation (P4) uses `nano_banana_pro`:**
- Petal first: references = the best 3–6 original photos. Prompt: the Style Bible + the photo-derived traits + "turnaround sheet, neutral pose, plain background". Generate 4 variants, let the Art Director pick one, and iterate.
- 🛑 **GATE 2:** show the user Petal's turnaround and expression sheet. Lock her only after the user approves.
- Then the other cast members, environments, and props. Batch these with `generate_image_batch`.
- Finally, the **key frames**: for every shot in every episode, a 9:16 `start_image` (and an `end_image` where the motion needs it) that composes the locked characters, environment, and props.

### Camera & Animation
13. **Storyboard Artist / Director of Photography**: breaks each script into **4–7 shots** (each 3–8s, totalling exactly 30s). For each shot: lens, framing, camera move, lighting, character action, and key frame description. Keep the main action in the centre-safe area, away from Reels UI (avoid the top 220px and the bottom 420px for faces and text).
14. **Animation Director**: writes the motion prompt for each shot. Use real animation principles: anticipation, squash and stretch, follow-through, appeal, and senior-dog-specific motion (a slower gait, a careful sit, a tail wag that involves the whole body). Every shot needs **one clear performance beat**.
15. **Dailies Supervisor (REVIEWER)** extracts frames with `ffmpeg -vf fps=4` and reviews them in a LOOP.
    **Rubric (threshold 8):** Character consistency vs the locked sheets · Motion quality and physics · Performance / acting · Composition and camera · Artefacts (morphing, flicker, limb errors) · Matches the storyboard intent · Continuity with the adjacent shots.

**Video generation (P6) uses `seedance_2_5`:**
- `mode: "omni_reference"`, `aspect_ratio: "9:16"`. Medias: `start_image` = the shot's key frame, an optional `end_image`, and `image_references` = the turnarounds of every character in the shot plus the environment plate.
- Set `duration` to the storyboard length. Set `generate_audio: false` (the Sound department owns audio), unless a shot needs synced vocal or foley reference.
- Run a draft pass first (`draft: true`). After it passes review, finalise at 1080p with `draft_job_id`. Use `bitrate_mode: "high"` for the final render.
- If a shot fails twice for consistency, regenerate its key frame first, then the video.

### Sound Department
16. **Composer**: writes a **series theme** (a 4-bar playful motif: oud + pizzicato strings + soft hand percussion, a Dubai flavour inside a family-film score), with an arrangement for each episode that hits the story beats at timecode.
17. **Sound Designer / Foley Artist**: plans the cue sheet for each episode: paw taps on marble, sand shuffles, abra engine, souk ambience, cat hiss, cartoon whooshes and stingers, plus Petal's signature sleepy "hmph" sigh.
18. **Re-recording Mixer / Sound Supervisor (REVIEWER)** reviews the BGM (background music) and all recordings in a LOOP:
    - Checks loudness with `ffmpeg -af ebur128` (target **−14 LUFS integrated**, true peak ≤ **−1 dBTP**, for Instagram).
    - Confirms dialogue and vocals sit above the music, with ducking on story beats.
    - Checks that the music hits picture (stingers within ±2 frames of the action), and that there are no clicks, clipping, or abrupt cut-offs.
    - Confirms the loop point: the last 0.5s of audio flows into the first 0.5s.
    - **Rubric (threshold 8.5):** Emotional fit · Sync to picture · Mix clarity · Loudness compliance · Theme consistency across episodes · Loop seamlessness.
- Generate the music and SFX with `generate_audio`, then render stems to `production/sound/epXX/`.

### Post-Production
19. **Editor**: assembles each episode in `ffmpeg`:
    - Concatenates the shots, with cuts on action, J/L cuts for sound, and a 0–3 frame trim where needed. Exact length: **30.0s** (±0.2s).
    - Lays in the music, SFX, and vocal stems from the mix.
    - Burns in **captions** in a bold rounded font with a dark outline, using a safe-area layout. Adds the on-screen hook text at 0–2s.
    - Applies a colour pass (a light shared LUT or a curves grade so all 5 episodes match).
    - Exports H.264 High, 1080×1920, 30fps, ~12–16 Mbps, AAC 48kHz 320kbps, with `+faststart`.
    - Also exports a **cover frame** (1080×1920 PNG) and a **3s silent preview GIF**.
20. **Colourist**: shot-to-shot colour matching and the final series-wide grade.
21. **Final Cut Review Panel (REVIEWER)**: Showrunner + Editor-in-Chief + the Instagram Growth Strategist, in a LOOP.
    **Rubric (threshold 8.5):** Pacing · Hook · Story clarity on mute · Comedy timing · Emotional beat lands · Seamless loop · Technical spec compliance · Series consistency.
    Run `virality_predictor` on each final cut, then fix the weakest predicted retention moment and re-run.

---

## 6. DELIVERY PACKAGE (P9)

```
deliverables/
  ep01_<slug>/  ep01_final.mp4  ep01_cover.png  ep01_preview.gif  ep01_caption.txt (caption + 15 hashtags + 3 hook variants)
  ... ep05
  series_bible.md
  character_sheets/  (all locked turnarounds + expression sheets)
  posting_plan.md    (posting order, best Dubai posting times, Story teaser ideas, pinned-comment prompts)
  production_report.md (scores per loop iteration, credits spent, known compromises)
```

Commit and push everything when you finish. Give the user a short summary with links to the generated videos.

---

## 7. QUALITY BAR & FAILURE RULES

- **Petal must be recognisable as Petal** in every frame. If likeness drops, stop and fix that shot before anything else.
- Prefer fewer, better shots over more, weaker ones. A great 4-shot episode beats a mediocre 7-shot episode.
- Never ship a frame with an anatomy artefact on a main character.
- If a tool or model is unavailable, pick the closest Higgsfield alternative (use `models_explore` with `action: "recommend"`), log why, and continue.
- Be honest in `production_report.md` about what fell short of the bar.

---

## 8. START

1. Read `refs/petal/` and write `production/story/petal_visual_traits.md`: breed, coat, markings, eyes, ears, body, and age signs.
2. Run P1 → P2. Present the **series bible + 5 scripts + the engagement scores** at 🛑 **GATE 1**.
3. After approval, run P3 → P4 and present Petal's sheets at 🛑 **GATE 2**.
4. After approval, run P5 → P9 fully autonomously.

Begin now.
