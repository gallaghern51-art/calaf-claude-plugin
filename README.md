# Calaf for Claude

[Calaf](https://calaf.ai) is a recruiting manager for MBA students: one book
that holds your target firms, the people you know there, your applications and
interview rounds, your meetings and follow-ups, and your interview prep. This
plugin connects Claude to your own Calaf account and teaches Claude how to run
the recruiting loop with it: plan your day, prep for a coffee chat or an
interview, log what happened, drill your flashcards, and turn research or a
document into content in your book.

You need a Calaf account with active access (a trial or a paid plan; see
[calaf.ai](https://calaf.ai)).

## What you get

**The Calaf connector.** The plugin connects Claude to Calaf's MCP server at
`https://calaf.ai/api/mcp-account`. After you install the plugin, connect it
from the plugin's **Connectors** tab (claude.ai, desktop, Cowork) or with
`/mcp` (Claude Code). You sign in on Calaf's own consent screen with OAuth;
Claude never sees your Calaf password, and you can disconnect at any time.

**Interactive cards (MCP Apps).** In Claude on the web and desktop, every
Calaf tool shows its result as an interactive card in the conversation:

- **Your day**: overdue tasks, follow-ups going cold, interviews and
  deadlines, and meetings waiting for an outcome, with Done, Snooze and
  It-happened buttons.
- **Rehearsal**: your due flashcards; reveal each one and grade it
  Again, Hard, Good or Easy. Grades save to the same schedule the Calaf app
  uses.
- **Staged deck**: a deck Claude wrote from your document; remove cards,
  then confirm or discard it in place.
- **Briefs**: the interview brief for one firm, the pre-chat brief for one
  person, and a side-by-side firm comparison.
- **Lists and records**: tasks, people, firms, pipeline, meetings, notes,
  templates and search results, and one contact, firm or application with
  forms for the next write.

Every button calls the same tool Claude would, under the same rules, and
Claude is told what you pressed. Clients without MCP Apps, including Claude
Code in the terminal, get the same facts as text.

**Skills.** Seven skills teach Claude the workflows:

| Skill | Use it when you say something like |
| --- | --- |
| `calaf-book` | anything about your Calaf book; the rules every other skill follows |
| `daily-briefing` | "what's on my plate today?" |
| `interview-prep` | "prep me for my Evercore interview" |
| `coffee-chat-prep` | "I have coffee with Sarah Chen tomorrow" |
| `log-interaction` | "log that I talked to David this morning" |
| `deck-from-document` | "turn this two-pager into flashcards" |
| `research-to-book` | "build me a list of 30 lower-middle-market PE funds" |

In Claude Code and Cowork, the plugin also includes a `firm-researcher`
agent that researches one firm from public sources and writes the sourced
result to your firm page.

## How Claude treats your book

- Everything runs as you, under your own account's permissions. Claude can
  only reach your book, never anyone else's.
- People are never added directly. Contacts Claude proposes arrive as a batch
  you review in Calaf under **Network**, and nothing reaches your contacts
  until you accept it.
- Your own values are never overwritten. Claude fills empty fields only and
  reports any conflict back to you.
- Claude can edit or remove only what Claude itself wrote, and can undo its
  recent writes when you ask.
- Firm research needs sources. A claim without a source is dropped, and deal
  terms that no source discloses stay empty rather than estimated.

## Data

When you use the plugin, Claude sends Calaf the requests you make: for
example the name of a firm or contact to look up, a note or touchpoint to
record, a flashcard grade, or research to save. Those go only to your Calaf
account at `calaf.ai`, over HTTPS, and are stored in your book like anything
you enter in the app. Calaf returns the records you asked for. The plugin
itself stores nothing, runs no local code, and sends nothing anywhere else.
The `firm-researcher` agent reads public web pages about a firm through
Claude's own web tools before it writes to Calaf.

Calaf's handling of your data is described in the
[Privacy Policy](https://calaf.ai/privacy); use of the service is governed by
the [Terms](https://calaf.ai/terms).

## Support

Setup guide: [calaf.ai/guide/assistant](https://calaf.ai/guide/assistant) ·
Questions or problems: **support@calaf.ai**
