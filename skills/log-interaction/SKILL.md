---
name: log-interaction
description: Record a networking interaction, meeting outcome, application move or follow-up in the user's Calaf book. Use when the user says they had coffee, a call, an event, sent outreach, got a reply, finished an interview round, got an offer or rejection, want to book a chat, or want a follow-up reminder.
---

# Logging what happened

Pick the tool by what happened:

| What happened | Tool |
| --- | --- |
| A chat, call, email, reply or event with someone already in the book | `log_touchpoint` |
| A meeting that was booked in Calaf and has now happened, was a no-show, or was cancelled | `complete_meeting` |
| A chat or firm event in the future | `schedule_meeting` (one contact or one firm, never both) |
| An interview round booked or held | `schedule_interview` |
| An application submitted, moved, offered or rejected | `add_application` or `update_application` |
| Something to do by a date | `add_task` |

## log_touchpoint

- Ask for when it happened if the user didn't say, and pass `at` with
  `time_zone` for chats and events so it lands on the calendar at the right
  time. Don't guess a time.
- Offer `follow_up_in_days` (the follow-up appears on the user's calendar) and
  `thank_you_task` for a next-day thank-you.
- A chat that hasn't happened yet is refused: book it with `schedule_meeting`.
- The person must already be in the book. If they aren't, offer to propose
  them through a seed (see `research-to-book`); they'll arrive as a staged
  batch the user reviews under **Network**.
- Touchpoints move the contact's stage forward automatically (Outreach Sent,
  Responded, Chatted), never backward. Don't set stages by hand to imitate
  this.

## After the write

Confirm in one line what landed, including any follow-up date. If the person
offered an intro or a referral, suggest a task to chase it.
