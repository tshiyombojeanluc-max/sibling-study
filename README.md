# Sibling Study Tracker

A weekly loop for turning topics your sibling's teachers send home into study notes and a
self-test. Live dashboard: https://claude.ai/code/artifact/8f0914ea-e048-4ee7-a140-3ed6e31c4eef

## How it works

1. **During the week** — add each topic on the [dashboard](https://claude.ai/code/artifact/8f0914ea-e048-4ee7-a140-3ed6e31c4eef)
   as teachers send it home. It's saved straight to ClickUp as a task in that subject's list
   (see below) — no file editing needed.
2. **Every hour** (cloud routines can't run more often than that) — a scheduled agent checks
   ClickUp for any topic still "to do", drafts study notes for it into
   `weeks/<week>/notes/<topic-slug>.md`, marks the task "complete" in ClickUp, pushes the notes
   to this repo, and emails tshiyombojeanluc@gmail.com the full text of each new note (so it can
   be copied/printed straight from the email). Most hourly runs find nothing new and exit quietly.
3. **Saturday, 2pm SAST** — a second scheduled agent queries that week's topics from ClickUp,
   writes `weeks/<week>/test.md` (10-15 mixed-difficulty questions) and `answer-key.md`, pushes
   both, and emails a summary + repo link.

## Where topics live (ClickUp)

Workspace → space **flipping cars** → folder **Sibling Study** → one list per subject:

| Subject   | List ID       |
|-----------|---------------|
| Math      | 901219680446  |
| Science   | 901219680452  |
| English   | 901219680453  |
| History   | 901219680454  |
| Geography | 901219680455  |
| Other     | 901219680456  |

Each topic is a task named after the topic, with `due_date` set to the Monday of the week it
belongs to (that's how "this week's topics" gets queried — not a real deadline). Task status
tracks note progress: `to do` → not drafted yet, `complete` → notes written.

## Folder layout

```
weeks/
  2026-W30/
    notes/           <- daily-generated study notes, one file per topic
    test.md          <- generated Saturday
    answer-key.md    <- generated Saturday
```

Topics themselves live in ClickUp, not in this repo — the dashboard and both scheduled agents
read/write there directly. ISO week folders (`2026-W31`, etc.) are created automatically as
needed (`date -u +%G-W%V`).

*(This tracker briefly used Notion for topic storage before moving to ClickUp on 2026-07-19,
after hitting Notion's free-plan query quota during testing.)*
