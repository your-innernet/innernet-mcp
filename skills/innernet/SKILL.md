---
name: innernet
description: The user's one memory across every AI tool (innernet.live). Use when a conversation touches a project the user keeps in innernet — its product, strategy, roadmap, brand, design, code, or past decisions — when they ask what was decided or where things stand, when work produces a decision or insight worth keeping, or when you learn something durable about the user themselves.
---

innernet is connected to this conversation as an MCP server. It holds the user's
versioned memory: one context map per project, a personal memory about the user,
and each project's task list. Every AI tool they use reads and writes the same
memory, so what you save here is what their other tools see next.

## before you answer about a project

1. Find the project: `innernet_list_projects` returns each map's slug and one line.
   If the user names one, match it; if the conversation clearly belongs to one, load it
   without asking.
2. Load it lean: `innernet_load_project { slug }`. You get the map's spine — one line
   per dimension — plus a `capture_protocol` written for that project. Follow it.
3. Answer a specific question from a slice, not the whole cabinet:
   `innernet_context { slug, intent }` with the user's ask verbatim returns the focus,
   its periphery, and `retrieval_advice` naming what to read next.
   `innernet_get_dimension { project_slug, dimension_name }` expands one dimension in full.
4. When the user asks what innernet knows in general, `search { query }` runs full-text
   search across every map, and `fetch { id }` returns one project whole.

Never pull full bodies you will not use. Let innernet drive retrieval.

## when work produces something worth keeping

- A decision, a direction, a corrected fact, a plan: `innernet_save_context`. Write the
  present. If what you save supersedes something a dimension states, replace it in the
  body — never leave old and new side by side — and add ONE dated line under a
  `## history` heading at the end of that dimension:
  `- YYYY-MM-DD — what changed: was … → now …`.
- A quick note that should fold into the map later, when you are unsure where it
  belongs: `innernet_capture`. Netti files it.
- Something about the USER (a preference, a tool they rely on, a person in their life,
  how or when they work, a standing instruction): `innernet_self_capture`, and mention
  briefly that you noted it. If the user would rather it not be kept, do not save it.
  Several captures piled up → `innernet_self_sync` folds them into facts.
  Personalising tone or defaults would help → read `innernet_self_facts`. Each fact
  says how it rests on what was said (`voice`): "said" is the user's own words,
  "reported" an AI's note of what they said or did, "inferred" innernet's reading.
  Speak for the user, or quote them, only from "said".
- Unsure whether it is about the user or a project: `innernet_triage` routes it.

## who said it

innernet keeps the user's words apart from yours, so it never tells them "you said"
about something an AI wrote.

- What you write in `content` is kept as your note: what you saw, did or suggested,
  in your own voice. Never write your own work as the user's ("I removed the blur
  from the header" is yours, not theirs), and a proposal of yours is not their
  decision until they say so.
- When the note is about something the user said, decided, prefers or is, also pass
  their exact words, copied from their message, in `user_words` (on `innernet_capture`,
  `innernet_self_capture` and `innernet_triage`). Only those are kept as theirs, so
  never put a summary or a paraphrase there.

## tasks

Each project carries a task list: `innernet_task_list`, `innernet_task_create`,
`innernet_task_update`, `innernet_task_complete`. When the user finishes something the
list tracks, complete it; when they commit to something new, add it.

## how to carry it

- Keep it light. Save what matters without turning the conversation into bookkeeping,
  and say in a few words what you saved and where, so the user always knows.
- Surface a relevant memory when it helps. Flag anything that looks stale or
  contradicted instead of asserting it.
- If innernet asks for authentication, the user signs in in their browser through
  the plugin's connection. Never ask them to paste an API key or token into the chat.

## when not to use it

- Small talk, or a topic the user has no project for and nothing durable was said.
- The user asks you not to remember something — then do not save it.
