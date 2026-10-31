---
name: "filmlab-schnittplatz"
description: "Use when a person wants to hand a FilmLab timeline to DaVinci Resolve, Final Cut Pro or Premiere Pro, or render a FilmLab sequence locally with its media and provenance."
---
<!-- Generated from shared/agenten-weg.ts — do not edit; run: node --experimental-strip-types scripts/agenten-skill/erzeuge.mjs -->

# filmlab-schnittplatz

## 1. Choose the editing software and format

For Resolve and Final Cut choose fcpxml. For Premiere Pro choose edl: Premiere does not read fcpxml, and OTIO import is only available in Premiere Pro Beta. FilmLab's EDL has no paths (relink by clip name), no transitions and at most four audio channels. FilmLab does not generate Final Cut legacy XML (xmeml). lab_schnitt_export provides the editing file at no cost.

## 2. Keep generated material private until release

Ask whether generated material may stay in FilmLab's cloud. If it must stay private until release, set lab_speicherort to lokal (this computer) or server (the studio's shared storage, such as a NAS or Avid NEXIS) BEFORE generating; it applies to material generated from then on. Each new file is then only parked for pickup: the Resolve panel, FilmLab Drop (Final Cut Pro, Avid, Premiere Pro) and filmlab_abholen in the local bridge store it in the configured folder, check it and confirm. FilmLab keeps a private working copy, signed access only, so export, sound mix and chains keep working. When the person says the project is finished or published, call lab_speicherort with abschliessen: true: FilmLab then deletes all working copies, and from then on its server export, local export and lab_schnitt_export cannot use that material. Copies are also deleted when the period in abholfrist_tage ends. Never close a project without the person's explicit yes, and never with auch_offene unless they agree that unpicked files are lost.

## 3. Hand over a local timeline with its media

If the local FilmLab bridge (filmlab_export_lokal) is available, use it with timeline set to the chosen format instead of downloading individual clips: it writes the timeline next to a media folder of readable hardlinks and the provenance document, and refuses when a source is missing. It currently needs the local export from a FilmLab repository checkout; the installer does not ship it yet. Without it, give the person the file from lab_schnitt_export: its media point to FilmLab URLs and are relinked by file name in the editing software.

## 4. Choose local render or server export

The default is the server export: lab_start_export, then follow lab_get_export. Alpha, portrait 9:16 derivatives and sequences with a dub render always stay on the server. Where the local bridge is available (see the previous step) and delivery time matters, render on this computer with filmlab_export_lokal without timeline, and read progress with stand: true.

## 5. Explain provenance before handing over

Tell the person before handover: the provenance document describes only the file as exported. If the file is edited elsewhere afterwards, that document no longer describes it. For a published version, bring the cut back into FilmLab through the Resolve return path and export again; otherwise the person carries the AI disclosure for the edited file themselves.

## 6. Prepare Resolve before import

Set the Resolve project's frame rate to the timeline's rate BEFORE importing; Resolve uses the project rate. Resolve rejects the entire timeline when a source is missing; the local timeline export therefore stops with exit code 5 and writes no file. Restore the missing sources before trying again.

## Rules

MONEY: name the price before a paid call and wait for the person's yes. Never auto-retry a video. For more than a handful of paid items propose ONE auto run (lab_auto_lauf) with a credit cap; freigeben only after an explicit yes. Reservations are never refunded. Under budget pressure lower the resolution, never the runtime. On budget_exceeded stop and report finished, open and the minimum budget; beenden when done.

SHOW RESULTS TO THE PERSON: the person often does NOT see tool results — only you do. Put every `karte_ansehen` link into your reply, for every finished image and every finished clip (clips: lab_job_status type video or lab_contact_sheet).

ERRORS carry `fehler` and `note` (jobs: `fehler_klasse`, `fehler_note`): follow the note.

PROMPT CHECK: lab_job_status shows `abgleich` (pass | mismatch | unverified | laeuft, with `issues`); report it in one line. On mismatch offer AT MOST ONE retry per original, the new prompt led by the failed claim; never retry a retry.

CHAINS: several clips go through lab_verkettung (plan → preis → starten after the yes). Continuous scene → one chain with schnitt; every clip is checked before the next starts and the chain stops on a deviation. Follow-up clips are text-to-video: give character_refs/location_id for continuity. Separate scenes → parallel.

WAIT with wait_s on lab_get_job / lab_job_status instead of polling.
