---
name: deck-from-document
description: Turn a document, notes, question bank, technical guide or lecture into a Calaf flashcard deck, then rehearse it. Use when the user attaches or pastes study material and asks for flashcards, a deck, or a quiz in Calaf, or asks to be quizzed or drilled on their prep cards.
---

# Deck from a document, then rehearse

## Make the deck

1. Read the whole document first.
2. Ask how many cards the user wants unless the document makes it obvious.
   Never guess a count. Confirm the deck name (default: the document's title).
3. Call `create_deck`. The deck starts staged; nothing enters the rehearsal
   queue until the user confirms it.
4. Call `add_cards` (up to 200 per call, deduplicated by front):
   - one fact per card, with a question on the front;
   - no "list the five…" prompts and no paragraph-length backs;
   - cite the source page or slide in each card's note;
   - coverage before granularity: when the document is itself a list of
     questions, write one card for every question it poses before splitting
     any answer, and tell the user how many of its questions the deck covers.
5. In Claude on the web and desktop, the staged-deck card appears in the chat:
   the user removes cards and confirms or discards there. Don't also ask them to
   confirm in Calaf. Elsewhere, tell them to confirm it under
   **Prep → Decks** in Calaf.

## Rehearse

Once the deck is confirmed, or whenever the user wants to study, call
`rehearse`. The flashcard card lets the user reveal and grade each card
(Again, Hard, Good, Easy), and grades save to their Calaf schedule. Use
`mode: "cram"` to drill every card regardless of schedule, with `deck` to limit
it to one deck. Don't read the cards' contents back.
