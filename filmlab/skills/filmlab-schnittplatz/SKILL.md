---
name: "filmlab-schnittplatz"
description: "Use when a person wants to hand a FilmLab timeline to DaVinci Resolve, Final Cut Pro or Premiere Pro, or render a FilmLab sequence locally with its media and provenance."
---
<!-- Generated from shared/agenten-weg.ts — do not edit; run: node --experimental-strip-types scripts/agenten-skill/erzeuge.mjs -->

# filmlab-schnittplatz

## 1. Choose the editing software and format

For Resolve and Final Cut choose fcpxml. For Premiere Pro choose edl: Premiere does not read fcpxml, and OTIO import is only available in Premiere Pro Beta. FilmLab's EDL has no paths (relink by clip name), no transitions and at most four audio channels. FilmLab does not generate Final Cut legacy XML (xmeml). lab_schnitt_export provides the editing file at no cost.

## 2. Hand over a local timeline with its media

If the local FilmLab bridge (filmlab_export_lokal) is available, use it with timeline set to the chosen format instead of downloading individual clips: it writes the timeline next to a media folder of readable hardlinks and the provenance document, and refuses when a source is missing. It currently needs the local export from a FilmLab repository checkout; the installer does not ship it yet. Without it, give the person the file from lab_schnitt_export: its media point to FilmLab URLs and are relinked by file name in the editing software.

## 3. Choose local render or server export

The default is the server export: lab_start_export, then follow lab_get_export. Alpha, portrait 9:16 derivatives and sequences with a dub render always stay on the server. Where the local bridge is available (see the previous step) and delivery time matters, render on this computer with filmlab_export_lokal without timeline, and read progress with stand: true.

## 4. Explain provenance before handing over

Tell the person before handover: the provenance document describes only the file as exported. If the file is edited elsewhere afterwards, that document no longer describes it. For a published version, bring the cut back into FilmLab through the Resolve return path and export again; otherwise the person carries the AI disclosure for the edited file themselves.

## 5. Prepare Resolve before import

Set the Resolve project's frame rate to the timeline's rate BEFORE importing; Resolve uses the project rate. Resolve rejects the entire timeline when a source is missing; the local timeline export therefore stops with exit code 5 and writes no file. Restore the missing sources before trying again.

## Rules

MONEY: name the price before a paid call and wait for the person's yes. Never auto-retry a video. For more than a handful of paid items propose ONE auto run (lab_auto_lauf) with a credit cap; freigeben only after an explicit yes. Reservations are never refunded. Under budget pressure lower the resolution, never the runtime. On budget_exceeded stop and report finished, open and the minimum budget; beenden when done.

SHOW RESULTS TO THE PERSON: the person often does NOT see tool results — only you do. Put every `karte_ansehen` link into your reply, for every finished image and every finished clip (clips: lab_job_status type video or lab_contact_sheet).

ERRORS carry `fehler` and `note` (jobs: `fehler_klasse`, `fehler_note`): follow the note.

PROMPT CHECK: lab_job_status shows `abgleich` (pass | mismatch | unverified | laeuft, with `issues`); report it in one line. On mismatch offer AT MOST ONE retry per original, the new prompt led by the failed claim; never retry a retry.

CHAINS: several clips go through lab_verkettung (plan → preis → starten after the yes). Continuous scene → one chain with schnitt; every clip is checked before the next starts and the chain stops on a deviation. Follow-up clips are text-to-video: give character_refs/location_id for continuity. Separate scenes → parallel.

WAIT with wait_s on lab_get_job / lab_job_status instead of polling.
