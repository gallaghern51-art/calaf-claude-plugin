---
name: interview-prep
description: Prepare the user for an interview, superday or recruiting event at one firm using their Calaf book. Use when the user says prep me for my interview at a firm, asks what to know before a round, wants talking points or a why-this-firm answer, or wants to drill questions for a specific firm.
---

# Interview prep for one firm

1. Call `interview_brief` with the firm as the book names it (use `search`
   first if unsure of the spelling). It returns the application and its
   rounds, how the firm runs its process, the next key dates, the user's people
   there with the last touch, talking points, prep readiness, open tasks and
   notes. The card shows all of it.
2. Tell the user, in a few lines:
   - what to expect: rounds, format, timing;
   - who they know there and what to thank or mention for each;
   - two or three talking points worth raising. Deals come with five brackets
     (deal size, consideration, valuation, strategic rationale, economic
     trend); a null bracket means no source discloses it, so never fill it in.
     If the result carries `deals_disclaimer`, say those deals were researched
     by AI and should be verified before being cited in the room.
3. Close the prep gaps:
   - For firm-specific questions with no answer, offer to draft one in the
     user's voice with `draft_prep_answer`. It fills only empty answers and
     marks them Draft. Improvements to an answer the user already wrote belong
     in the chat, not in the book.
   - If cards are due, offer `rehearse` with `mode: "cram"`, limited to the
     firm's deck when one exists, so the user can drill in the chat.
4. If the user wants a why-this-firm answer, build it from the book: their
   people there, the groups they target, the deals, the notes. Say which
   entries each point rests on.
5. End by asking which part to go deeper on. Offer a thank-you task with
   `add_task` for the day after the interview.

For a side-by-side view of several firms, use `compare_firms` (up to eight).
