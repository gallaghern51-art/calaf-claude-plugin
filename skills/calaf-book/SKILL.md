---
name: calaf-book
description: Work in the user's Calaf recruiting book (firms, contacts, applications, interviews, meetings, tasks, notes, templates, interview prep). Use whenever the user mentions Calaf, their recruiting book, target firms, networking contacts, coffee chats, applications, superdays, prep cards, or asks Claude to read or change anything in Calaf.
---

# Working in a Calaf book

Calaf is the user's MBA recruiting manager. The `calaf` connector is signed in
as the user's own account, so every read and write is theirs. This skill holds
the rules every other Calaf skill relies on.

## Start of a conversation

1. Call `get_profile` once per conversation before giving advice: it returns
   who the user is (school, class, workspaces), where they are in the
   recruiting cycle, what this month usually means for their track, and the
   next key dates for their target firms.
2. For "what should I do" questions, call `get_briefing`.
3. When the user names something and you don't know whether it's a person, a
   firm, a deck or a note, call `search` first. Use the spelling the book uses
   before calling any write tool.

## The cards (MCP Apps)

In Claude on the web and desktop, each Calaf tool result renders as an
interactive card: lists with row actions, records with forms, the briefing,
flashcard rehearsal and the staged deck. The user can act in the card
directly, and you are told what they pressed.

- Summarise what matters and propose the next step. Don't read the card's rows
  back to the user; they can see them.
- When the user acts in a card (marks a task done, grades a card, confirms a
  deck), build on that instead of repeating the action.
- In clients without cards (Claude Code in a terminal), the same facts come
  back as text: present the few lines that matter, not the whole payload.

## Rules the server enforces (tell the user plainly when one applies)

1. **People are never created directly.** Contacts are proposed through a seed
   (`import_seed`) and arrive as a staged batch the user reviews in Calaf under
   **Network**. `log_touchpoint`, `schedule_meeting` and `update_contact` work
   only on people already in the book.
2. **The user's own values are never overwritten.** Identity fields and prose
   fill only where empty; conflicts come back in the result. Show them to the
   user and let them decide.
3. **Facets the user names are set exactly.** Statuses, priorities, warmth and
   dates the user asks for go in as stated.
4. **Edits and removals reach only what the assistant wrote**: notes,
   templates, work-log items and staged decks. If a tool refuses because a row
   is the user's, say so; don't look for a workaround.
5. **Sourced claims only.** Firm research needs a source per claim. A deal
   term no source discloses stays null; never estimate one.
6. **Deals researched by AI carry `deals_disclaimer`.** When a result includes
   it, tell the user those deals were researched by AI and that they should
   verify the terms before citing them in a room.
7. **Nothing the user wrote is deleted.** Archive is the only end state for a
   workspace. `undo_last_write` lists and removes only the assistant's own
   recent writes, and only after the user asks.

## Choosing a tool

| The user wants to… | Call |
| --- | --- |
| Know what needs them today | `get_briefing` |
| Find anything by name | `search` |
| Open one person / firm / application | `get_contact` / `get_firm` / `get_application` |
| List people, firms, pipeline, tasks, notes, templates | `get_contacts`, `get_firms`, `get_applications`, `get_tasks`, `get_notes`, `get_templates` |
| Record a chat, call, email or event that happened | `log_touchpoint` |
| Book a future chat or firm event | `schedule_meeting` |
| Say how a booked meeting went | `complete_meeting` |
| Add something to their calendar | `add_task` |
| Track or move an application | `add_application`, `update_application`, `schedule_interview` |
| Prep for a firm's interview | `interview_brief` |
| Prep for a chat with a person | `get_meeting_brief`, `get_contact` |
| Compare targets | `compare_firms` |
| Study or drill | `rehearse` |
| Make flashcards from material | `create_deck`, then `add_cards` |
| Add many firms, templates, prep questions or people at once | `get_seed_format` → `validate_seed` → `import_seed` |
| Save sourced research on one firm | `get_profile_schema` → `get_firm_profile` → `submit_firm_profile` |
| See what changed recently | `get_changes` |
| Take back something the assistant wrote | `undo_last_write` |
| See the Network Commons | `get_commons_org`, `get_commons_events`, `get_commons_schools`, `get_commons_questions` |

## Writing well into the book

- Ask rather than guess when a write needs a fact the user hasn't given: a
  date, a time zone, which of two contacts with the same name.
- After a write, confirm in one line what landed and offer the obvious next
  step, such as a follow-up task after a logged chat.
- The user's interview answers are in their own voice. `draft_prep_answer`
  fills only empty answers and marks them Draft; suggest improvements to an
  existing answer in the chat instead of writing them into the book.
