---
name: daily-briefing
description: Plan the user's recruiting day or week from their Calaf book. Use when the user asks what's on their plate, what to do today, for a morning check-in, a weekly review, what changed this week, or what they're behind on.
---

# Daily briefing and weekly review

## Today

1. Call `get_briefing`. Call `get_profile` too if you haven't read it in this
   conversation; its cycle phase tells you what this month is for.
2. The briefing card already lists every item. Don't read it back. Pick the
   three items that matter most today and give a plan of at most three
   bullets, one item each, leaving the rest to the card. Priority order:
   - interviews and application deadlines in the next few days;
   - follow-ups due and contacts going cold;
   - overdue tasks, then everything else.
3. Offer to do the pieces you can:
   - draft the overdue follow-up messages (as text in the chat; Calaf doesn't
     send email);
   - push tasks that can wait with `snooze_task`, after the user agrees;
   - settle past meetings still waiting for an outcome with `complete_meeting`,
     once the user tells you what happened;
   - start a rehearsal with `rehearse` if cards are due.

## This week

1. Call `get_changes` with `days: 7`, then `get_briefing`.
2. Summarise the week in five lines at most: what moved in the pipeline, who the
   user talked to, what the assistant wrote to the book, and what went quiet.
3. Propose three targets for next week (people to reach, applications to move,
   prep to close). Offer to add them with `add_task`, each with a due date the
   user agrees to.

## Don't

- Don't invent urgency the book doesn't show.
- Don't mark tasks done or snooze them without the user saying so; the card's
  buttons are there for that.
