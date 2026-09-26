---
name: research-to-book
description: Turn research into Calaf content in bulk - target firm lists, outreach templates, interview prep questions, and proposed contacts - through a validated Calaf seed file. Use when the user asks Claude to build a list of firms, stock their book, import research, add many firms or prep questions at once, or export and improve a workspace.
---

# Research into the book, through seeds

Bulk content enters Calaf as a seed: a JSON document in the `calaf_seed`
format that the app's own importer reads. The loop is always the same.

1. Call `list_workspaces` and agree with the user which workspace the content
   belongs in (or create one with `create_workspace`).
2. Call `get_seed_format` and follow it exactly.
3. Do the research. Include only what you can support; leave a field empty
   rather than guess.
4. Call `validate_seed` with the entire document as a string. `error` means
   nothing imports; `dropped` means that row or field is discarded. Fix every
   issue and validate again until it's clean.
5. For a bulk seed, show the user what it holds (counts and a few examples)
   and get a yes. When the user asked for exactly this content (one person,
   one firm), their request is the yes.
6. Call `import_seed`. It is additive and deduplicated: firms the book already
   has are enriched only where fields are empty, and re-importing lands nothing
   new.
7. Tell the user what landed. If the seed named people, they are **staged**,
   not added: tell the user to open Calaf → **Network** to accept, trim or
   discard the batch. A person must name an organization to be stageable.

## Improving an existing workspace

`export_seed` reads a workspace back out as a seed. It leaves people and
personal notes out unless asked. Improve it, validate, and re-import;
the user's own values are kept.

## One firm in depth

For deep, sourced research on one firm (overview, HQ, leadership, pay,
recruiting process, culture), use `get_profile_schema`, then
`get_firm_profile`, then `submit_firm_profile` with a source for every claim.
In Claude Code and Cowork, the `firm-researcher` agent does this end to end.
