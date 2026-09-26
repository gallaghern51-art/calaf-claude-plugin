---
name: coffee-chat-prep
description: Prepare the user for a coffee chat, networking call or informational interview with one person in their Calaf book. Use when the user mentions an upcoming chat, call or meeting with a named contact, asks what to ask someone, or wants a brief before talking to a banker, consultant or alum.
---

# Coffee-chat prep for one person

1. Call `get_contact` for the person (use `search` first if the name is
   ambiguous). If a meeting with them is booked, call `get_meeting_brief`; it
   defaults to the next booked meeting, and can be narrowed by contact. Call
   `get_firm` for their firm if the brief doesn't already cover it.
2. Give the user a short brief:
   - two lines on who the person is and how the relationship got here;
   - what the person is likely to ask the user (the brief's `expect` set
     pieces), with the user's three reasons for the firm if the brief has them;
   - what other members report about this person or firm on the Network
     Commons, when the brief includes `commons` (it is aggregated and never
     attributed; keep it that way);
   - one paragraph on the firm as it matters to this chat: recent deals,
     groups, recruiting timing. Pass on `deals_disclaimer` when present;
   - five questions to ask that show the user did the reading;
   - two things about the user that connect to this person.
3. If no brief exists yet, say so. The user writes or regenerates briefs in
   Calaf, and briefs are metered per day, so don't retry.
4. After the chat, offer to log it: see the `log-interaction` skill.
