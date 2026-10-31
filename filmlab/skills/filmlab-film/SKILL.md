---
name: "filmlab-film"
description: "Use when a person wants to turn a brief or existing media into a finished, editable film with FilmLab: plan, generate, check, edit, mix, grade and export."
---
<!-- Generated from shared/agenten-weg.ts — do not edit; run: node --experimental-strip-types scripts/agenten-skill/erzeuge.mjs -->

# filmlab-film

## 1. Sign in and choose the project

Check lab_whoami, then use lab_list_projects and lab_get_project to select the project, or lab_create_project to create it. Complete sign-in when requested. Respect its datenmodus: eu or frei. For eu, use lab_list_models with eu: true and only the permitted models; never switch the project out of EU mode to bypass a refusal.

## 2. Plan the shots, quote the price, get approval

Derive the shots from the brief and choose models from lab_list_models. Quote the total price before spending. For more than a handful of paid items, propose ONE lab_auto_lauf with a credit cap and obtain one explicit approval for that run; use freigeben only after that approval. Include the intended generation and export work in the plan. Outside an approved run, quote and obtain approval before each paid call.

## 3. Generate with continuity

Use lab_generate for images and lab_animate for individual clips. For connected scenes use lab_verkettung: plan, preis, then starten after approval. Keep a continuous scene in one chain with schnitt; provide character_refs and location_id for continuity. Separate scenes can run in parallel. Wait with wait_s on lab_get_job or lab_job_status instead of repeatedly polling.

## 4. Check and show every result

Read abgleich in lab_job_status and report pass, mismatch, unverified or laeuft with the issues in one line. On mismatch offer at most one new attempt per original, lead the new prompt with the failed claim, and never retry a retry or automatically retry a video. Put every karte_ansehen link in your reply, for images and clips; obtain a clip card through lab_job_status with type video or lab_contact_sheet.

## 5. Write the whole cut, then read it back

Read the existing cut with lab_get_sequence. Use lab_timeline_apply for the WHOLE cut, pass the revision you read as erwartete_revision, and retain each existing clip_id so its identity and inherited metadata survive. On revision_veraltet, read again and merge before writing. Read lab_get_sequence again after applying and check the result. Use the two groups below: perform the manifest operations yourself; for editor-only work direct the person to Murnau and IRO and say that the editor can do it. lab_fassungen reads or restores the automatically saved checkpoints; lab_wortzeiten supplies word timings when computing pause cuts.

WARNING: the manifest represents only one sequential row. Do not rebuild a cut containing V2+ clips through it: inherited tracks do not preserve overlapping start times. Refer that cut to Murnau. When splitting through the manifest, the second piece gets a new clip_id and inherits neither grade nor effects. Existing effects, keyframes and constant speed survive through retained clip_id, but the manifest cannot set them.

## 6. Mix the sound for delivery

Use lab_mix_render with the delivery loudness target: broadcast, web or youtube, and an auto_preset when appropriate. Wait for lab_get_job with wait_s, then report the measured result and any missed targets.

## 7. Finish the look

Use lab_grade_clip for the grade of a clip in the cut, or of the whole programme with programm: true; the export uses that grade. lab_grade only grades still images in the gallery. If grading will happen in Resolve, use lab_look_in_post to prepare that handover and follow the filmlab-schnittplatz skill.

## 8. Show the preview, then export

Before the final render, summarise the cut from lab_get_sequence (clips in order, lengths, transitions, bed, sound) next to the clip cards already shown, and tell the person they can watch and adjust it in the FilmLab editor (Murnau). After the person has reviewed it and the required spending approval is covered, use lab_start_export. Follow lab_get_export until completion, show the delivered file and its provenance, and close the lab_auto_lauf with beenden when done.

## Rules

MONEY: name the price before a paid call and wait for the person's yes. Never auto-retry a video. For more than a handful of paid items propose ONE auto run (lab_auto_lauf) with a credit cap; freigeben only after an explicit yes. Reservations are never refunded. Under budget pressure lower the resolution, never the runtime. On budget_exceeded stop and report finished, open and the minimum budget; beenden when done.

SHOW RESULTS TO THE PERSON: the person often does NOT see tool results — only you do. Put every `karte_ansehen` link into your reply, for every finished image and every finished clip (clips: lab_job_status type video or lab_contact_sheet).

ERRORS carry `fehler` and `note` (jobs: `fehler_klasse`, `fehler_note`): follow the note.

PROMPT CHECK: lab_job_status shows `abgleich` (pass | mismatch | unverified | laeuft, with `issues`); report it in one line. On mismatch offer AT MOST ONE retry per original, the new prompt led by the failed claim; never retry a retry.

CHAINS: several clips go through lab_verkettung (plan → preis → starten after the yes). Continuous scene → one chain with schnitt; every clip is checked before the next starts and the chain stops on a deviation. Follow-up clips are text-to-video: give character_refs/location_id for continuity. Separate scenes → parallel.

WAIT with wait_s on lab_get_job / lab_job_status instead of polling.

## Editing capabilities

### Through lab_timeline_apply

- `trim` (indirect): Set in_s, out_s and dauer_s by rewriting the whole manifest.
- `checkpoint` (yes): Automatic before every write; lab_fassungen reads and restores saved versions.
- `loeschen` (indirect): Omit the clip; start_time is recalculated.
- `entpausen` (indirect): Read lab_wortzeiten and compute the retained pieces yourself; there is no dedicated pause-cut tool.
- `bett` (partial): manifest.bett covers the whole cut, not a selected time range; use Murnau for a time range.
- `umsortieren` (yes): Change the order of entries in the manifest.
- `uebergang` (partial): Only dissolve, identical at every cut. The server render does not apply it; FCPXML export does. For per-cut transitions use Murnau and IRO.
- `teilen` (indirect): Use two entries of the same source with adjacent in_s/out_s; the new clip_id inherits neither grade nor effects.
- `einfuegen` (yes): Insert asset_key or video_id at a position in the sequential row.
- `uebernehmen` (yes): Use the video_id of a generated video.

### Editor-only actions

These actions are available in Murnau, by hand or via its assistant IRO (descriptions in German, from the playbook):

- `schneiden`: Einen Clip an der Abspielposition in zwei teilen.
- `punch`: Auf ein gesprochenes Wort einzoomen (Punch-in) — der Bildausschnitt wird für das Wort enger, sonst bewegt sich nichts.
- `titel`: Einen Titel (Text aufs Bild) setzen oder entfernen.
- `effekt`: Deckkraft, Größe, Lage, Drehung und Lautstärke eines Clips setzen, auch mit Keyframes.
- `tempo`: Das feste Tempo eines Videoclips setzen (0,0625× bis 16×, 1 = normal); sein Ton folgt.
- `speed-ramping`: Die Geschwindigkeit innerhalb eines Clips verändern.

### Not available


Before telling the person that something cannot be done, call lab_playbook with flaeche edit.
