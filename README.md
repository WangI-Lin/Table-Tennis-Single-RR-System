# Table Tennis Singles Round-Robin & Knockout Tournament System

**Tagline**: A cloud-based table-tennis singles tournament platform built on Google Sheets + Apps Script, fully ported from a mature Excel/VBA system, supporting real-time multi-user operation.

## Overview

This system is a cloud-based tournament management tool for table-tennis singles open tournaments, school/college cups, and club round-robins, designed for tournament organizers, chief referees, and tournament volunteers. The original system was a long-used Excel VBA workbook, and this project ports it in full to Google Apps Script so that multiple referees can enter scores and view brackets simultaneously online, no longer tied to a single Excel machine. The workflow automates everything from player roster import all the way to the bronze match, 5th-place playoff, and one-click medalist roster.

## Why This System

Traditional Excel-based scoring is single-machine — referees queue up to enter scores. This system uses Google Sheets for real-time collaboration, with dialog-based score entry that avoids accidental formula breakage. When new computers or OS versions break VBA macros, this system runs on pure Apps Script with no installation needed. Snake draw, knockout brackets, and bronze-match logic are complex and error-prone by hand; this system has built-in ITTF-standard snake draw, same-association exchange, and ITTF-standard KO seeding. The cascading-change problem from substitutions and rescheduling is solved by partial recomputation functions (Change Pool / Renew Tables). Post-tournament ranking and medalist calculation are automated using the ITTF ranking hierarchy (match points → head-to-head → game ratio → point ratio).

## Core Features

The full workflow lives under the custom menu "Table Tennis Single RR" in Google Sheets, executed in tournament order:

1. **Clean Data Book** — clear old data, prep for a new tournament
2. **Select Events** — pick which events will run this time via dialog
3. **Ranking and Grouping** — snake-draw seeding by ranking, with two modes: Ordinary Snake (randomization within rank level + automatic same-association swap) and Modified Snake (Beijing 2008 pure mechanical snake)
4. **Make Tables (RR + KO + tt)** — auto-generate round-robin tables, KO brackets, and per-event timetables
5. **Make TT** — merge all per-event timetables into the master schedule
6. **Make Match** — schedule matches per table
7. **Print Score** — print scorecards, simple RR slips, and per-player schedules
8. **Input Score** — dialog-based score entry with auto-writeback
9. **Fill Points & Rank** — auto-compute standings using ITTF tiebreaker hierarchy
10. **Final KO Draw** — draw advancers into knockout slots (auto / manual / avoid-adjacent-same-association)
11. **Medalist** — auto-produce the medalist roster

Additional capabilities include a decoupled global player database (`data_Common`) in a shared Google Sheets for easy long-term maintenance, per-event color coding, an unplayed-match counter, and configurable rules for bronze match, 5th-place match, ITTF bye, and qualifiers per group.

## Requirements

A Google account, Google Sheets edit access, and the latest Chrome / Edge / Safari browser are all that's needed. Developers additionally need Node.js ≥ 18 and clasp.

## Architecture

Google Sheets serves as the UI and data layer, with Apps Script V8 running the business logic in pure JavaScript. The system uses Spreadsheet Service for sheet I/O, Advanced Sheets API v4 for high-performance batch formatting, UI Service for menus and dialogs, and Properties Service to store the player database file ID. Over 30 `.bas` / `.frm` modules from the original VBA workbook have been fully ported, with the underlying algorithms (snake-draw ordering, KO position numbering, ITTF tiebreakers) faithfully preserved.

## License

MIT License — free for personal, modified, and commercial use. See [LICENSE](LICENSE).

## Contact

ilinwang0901@gmail.com
