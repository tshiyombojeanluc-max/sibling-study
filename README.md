# Sibling Study Tracker

A weekly loop for turning topics your sibling's teachers send home into study notes and a
self-test. Live dashboard: https://claude.ai/code/artifact/8f0914ea-e048-4ee7-a140-3ed6e31c4eef

## How it works

1. **During the week** — add each topic on the [dashboard](https://claude.ai/code/artifact/8f0914ea-e048-4ee7-a140-3ed6e31c4eef)
   as teachers send it home. It's saved straight to the "Sibling Study Topics" Notion database
   (`collection://3f23dd51-f8c4-4082-876d-b2188e0d4707`) — no file editing needed.
2. **Daily, ~6pm SAST** — a scheduled cloud agent checks Notion for any topic not yet marked
   "Done", drafts study notes for it into `weeks/<week>/notes/<topic-slug>.md`, marks it "Done"
   in Notion, pushes the notes to this repo, and emails tshiyombojeanluc@gmail.com the full text
   of each new note (so it can be copied/printed straight from the email).
3. **Saturday, 2pm SAST** — a second scheduled agent queries that week's topics from Notion,
   writes `weeks/<week>/test.md` (10-15 mixed-difficulty questions) and `answer-key.md`, pushes
   both, and emails a summary + repo link.

## Folder layout

```
weeks/
  2026-W30/
    notes/           <- daily-generated study notes, one file per topic
    test.md          <- generated Saturday
    answer-key.md    <- generated Saturday
```

Topics themselves live in Notion, not in this repo — the dashboard and both scheduled agents
read/write there directly. ISO week folders (`2026-W31`, etc.) are created automatically as
needed (`date -u +%G-W%V`).
