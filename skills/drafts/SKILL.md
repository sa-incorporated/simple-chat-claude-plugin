---
name: drafts
description: Review the items that wait for staff approval in Simple Chat - the customer replies that the @SC agent drafted, and the refund, cancel, order change, customer record and replacement order proposal cards. Use when the user asks what needs their approval, asks to send, approve, discard or reject a drafted reply, asks to approve or reject a proposal, or asks to start a refund, cancel, order change or customer record proposal for an order.
---

# Review the items that wait for approval

Two kinds of items wait for a staff member in Simple Chat:

- **Drafted replies.** Simple Chat's @SC agent drafts replies to customers.
- **Proposal cards.** The AI or a staff member proposes a refund, an order cancel, an order change, a customer record
  change or a replacement order for an order of the ticket.

A draft reaches the customer, and a card changes the order or the customer, only after the staff member clicks Confirm.
You cannot confirm for them.

A refund card, an order cancel card and a replacement order card move money. From Claude, the staff member can see
and reject these cards, and can start a refund card or an order cancel card. They cannot approve them from Claude: they
approve them in the Simple Chat dashboard.

1. **Find the items.** For drafts, call `list_inbox_conversations`, then `list_pending_customer_drafts` for each open
   conversation. For cards, call `list_staff_proposals`: with a conversationId for one ticket, or without one for the
   conversations of an inbox page. Without a conversationId, each of these calls reads one inbox page: while hasMore
   is true, call it again with offset set to nextOffset. When the user asks what needs their approval, show both. Show
   each draft with the customer, the ticket subject and a short preview. Show each card on one line: its kind, the
   order, the action and the amounts with their currency.
2. **Pick the item.** When the user names an item ("the late delivery one", "the refund for #1001"), match it to one
   draft or one card. When more than one fits, ask which one. When a ticket holds several drafts, pass that draft's
   clientMessageId. For a card, pass its proposalId.
3. **Decide.**
   - To send a draft, call `approve_pending_customer_message`. To discard it, call `reject_pending_customer_message`.
   - To approve an order change card or a customer record card, call `approve_staff_proposal`. Pass a staff field (for
     example a hold date or a new phone number) only when the user gives it; the card keeps its own values for the
     others. Pass notifyCustomer false only when the user asks for no customer message.
   - To approve a refund card, an order cancel card or a replacement order card, do not call a tool. Tell the user
     that these cards are approved in the Simple Chat dashboard, and give the ticketUrl of the card.
   - To reject a card of any kind, call `reject_staff_proposal`. A reject changes nothing in Shopify.

   Each call only makes a preview and shows a Confirm card with the facts. Nothing changes yet. For a card, read the
   preview to the user in a few lines: the action, and what Notify customer sends.
4. **Stop and let the user confirm.** Tell the user to read the card and click Confirm or Cancel. Do not call the tool
   again to confirm, and do not say that the reply was sent or the card was approved until the Confirm card or a later
   read shows it. When a Confirm fails because the card changed or somebody decided it, read the card again before
   you make a new preview.
5. **One item for each card.** When the user asks to decide several items, make one preview for each item. Each one
   needs its own click. A request to approve "without asking" does not change this.
6. **Only on request.** Approve, reject or start a card, and send or discard a draft, only when the user asks for
   that action on that item.

If no Confirm card shows, for example in Claude Code in a terminal, the user cannot confirm here. Give them the
ticketUrl, where they can decide the item in the Simple Chat dashboard.

## Start a proposal card

When the user asks for a refund, a cancel, an order change or a customer record change for an order of a ticket, call
`start_staff_proposal` with the order name that `get_customer_orders` gives for that ticket. The start changes nothing
in Shopify: it puts a card in the ticket, which waits for a staff decision as in step 3. Read the new card with
`list_staff_proposals`. After you start a refund card
or a cancel card, say that the approval is in the Simple Chat dashboard, and give the ticketUrl. A ticket has one card
of each kind for each order, and one customer record card for each customer: a waiting customer record card stops a
second one for another order of the same customer until staff decide it. Staff start a replacement order card in the
dashboard.

To get a new draft for a ticket, ask @SC with `consult_ticket_staff_agent`, as the inbox skill describes.
