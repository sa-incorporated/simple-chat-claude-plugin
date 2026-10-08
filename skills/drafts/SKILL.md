---
name: drafts
description: Review the customer replies that Simple Chat's @SC agent drafted and that wait for staff approval. Use when the user asks to see drafts that need approval, or to send, approve, discard or reject a drafted reply to a customer.
---

# Review drafted replies

Simple Chat's @SC agent drafts replies to customers, and a staff member approves each one. A draft reaches the
customer only after the staff member clicks Confirm. You cannot confirm for them.

1. **Find the drafts.** Call `list_inbox_conversations`, then `list_pending_customer_drafts` for each open
   conversation. Show each draft with the customer, the ticket subject and a short preview.
2. **Pick the draft.** When the user names a draft ("the late delivery one"), match it to one conversation. When more
   than one draft fits, ask which one. When a ticket holds several drafts, pass that draft's clientMessageId.
3. **Send or discard.**
   - To send, call `approve_pending_customer_message`.
   - To discard, call `reject_pending_customer_message`.

   Each call only makes a preview and shows a Confirm card with the draft and the customer. Nothing changes yet.
4. **Stop and let the user confirm.** Tell the user to read the card and click Confirm or Cancel. Do not call the tool
   again to confirm, and do not say that the reply was sent until the card or a later read shows it.
5. **One draft for each card.** When the user asks to send several drafts, make one preview for each draft. Each one
   needs its own click. A request to send "without asking" does not change this.

If no Confirm card shows, for example in Claude Code in a terminal, the user cannot confirm here. Give them the
ticketUrl, where they can send or discard the draft in the Simple Chat dashboard.

To get a new draft for a ticket, ask @SC with `consult_ticket_staff_agent`, as the inbox skill describes.
