# Sibling Study Tracker

A weekly loop for turning topics your sibling's teachers send home into study notes and a
self-test.

## How it works

1. **During the week** — whenever a teacher sends a topic, open
   `weeks/<current-week>/topics.md` and add it under the right subject heading.
2. **Get notes** — ask Claude Code (locally, any time) to read that file and write study
   notes into `weeks/<current-week>/notes/<topic-slug>.md`. Just say something like:
   _"generate notes for the new topic in weeks/2026-W30/topics.md"_.
3. **Saturday, 2pm SAST** — a scheduled cloud agent automatically:
   - reads that week's `topics.md` and whatever is in `notes/`
   - writes `test.md` (10-15 questions spanning the week's topics, mixed difficulty,
     appropriate for a middle/high school student) and `answer-key.md`
   - commits and pushes both files
   - emails tshiyombojeanluc@gmail.com a summary with a link to the repo

## Folder layout

```
weeks/
  2026-W30/
    topics.md       <- you fill this in during the week
    notes/           <- study notes, one file per topic
    test.md          <- generated Saturday
    answer-key.md    <- generated Saturday
_template/
  topics.md          <- copy this into a new weeks/<ISO-week>/ folder each week
```

ISO week folders look like `2026-W31`, `2026-W32`, etc. (`date -u +%G-W%V`). Start a new one
each Monday, or ask Claude Code to do it for you.
