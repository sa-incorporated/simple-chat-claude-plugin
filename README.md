# Simple Chat for Claude

Work the support inbox of your Shopify store from Claude. [Simple Chat](https://simple-chat.com) is the AI support
inbox for Shopify stores. This plugin connects Claude to your Simple Chat account. With it, you can:

- read and search customer conversations;
- check the orders of a customer;
- leave notes for your team, and claim tickets;
- queue a reply with your exact text, and approve the replies that you or the AI drafted;
- see and reject the refund, cancel, order change, customer record and replacement order proposals of a ticket;
- start a refund, cancel, order change or customer record proposal, and approve an order change or a customer record
  proposal;
- read the instructions of your store's AI, and change them and your FAQs;
- replay a topic to see why the AI did not resolve it.

## What you need

- A Shopify store with [Simple Chat](https://apps.shopify.com/simple-chat) installed. The plugin works on every
  Simple Chat plan. Topic replay needs the Premium plan.
- A staff account on that store. You connect as yourself, on one store.
- Claude on the web, the Claude desktop or mobile app, Cowork, or Claude Code.

## What the plugin contains

- **One connector**, `simple-chat`: the remote MCP server `https://mcp.simple-chat.com/mcp`, which SA Inc. operates.
  You sign in with OAuth. The plugin holds no key and no password.
- **Four skills** that tell Claude how to use the connector:
  - `get-started` checks the connection and shows what to ask.
  - `inbox` reads and searches conversations, customers and orders, makes internal changes to a ticket, and reads and
    changes the FAQs and the instructions of your store's AI.
  - `drafts` queues a reply with your exact text, sends or discards a drafted reply, and approves or rejects a proposal
    card, after you confirm. It also starts a proposal card.
  - `topic-replay` shows AI resolution by topic and runs a topic replay (Premium).

The plugin has no hooks, no scripts and no local programs. It runs nothing on your computer, and it sends data only to
`mcp.simple-chat.com`.

## Connect

1. Add the Simple Chat plugin to Claude. In Claude Code, run these two commands:

   ```text
   /plugin marketplace add sa-incorporated/simple-chat-claude-plugin
   /plugin install simple-chat@simple-chat
   ```

2. Connect the Simple Chat connector. On claude.ai and in the desktop app, open the plugin's **Connectors** tab. In
   Claude Code, run `/mcp`, choose `simple-chat` and sign in.
3. Type the address of your store, for example `your-store.myshopify.com`.
4. Approve the connection in your Shopify admin. The page shows the assistant, the store and your staff name.
5. Ask Claude: "Help me get started with Simple Chat."

## What you can ask

- "What's waiting for me in Simple Chat?"
- "Find the customer Avery Example and show their recent orders."
- "Open the conversation about the damaged teapot, leave an internal note that a replacement is approved, and claim
  it for me."
- "Show drafts that need my approval, then send the one for the late delivery question."
- "Show the drafts and proposals that need my approval."
- "Why is AI resolution low for Returns and refunds? Replay it for the last 90 days."

## You confirm before a customer gets a message or an order changes

Claude cannot send a message to a customer or change an order by itself. A reply that you ask Claude to queue waits as
a draft, as a reply that the AI drafted does. You can ask it to send or discard a drafted reply, to approve an order change or a customer record proposal, to reject a proposal, or to start a paid topic replay.
Simple Chat then shows a Confirm card in the conversation. Nothing happens until you click **Confirm**. Notes, claims,
pins and status changes stay inside Simple Chat, and the customer does not see them. A change of an FAQ or of the
instructions of your store's AI applies at once when you ask for it, with no Confirm card, and the other settings stay
in the Simple Chat dashboard.

Claude can also start a refund, cancel, order change or customer record proposal for an order of a ticket. A new
proposal changes nothing until a staff member approves it.

## No money moves from Claude

A refund, an order cancel and a replacement order move money. You cannot approve these proposals from Claude. Claude
shows the proposal and gives you the link to the ticket, and you approve it in the Simple Chat dashboard. The plugin
has no other payment tool: it cannot charge a customer.

## Where the Confirm card shows

The Confirm card shows in Claude on the web and in the Claude apps. Claude Code in a terminal cannot show the card.
There, Claude gives you the link to the ticket, and you send the draft or decide the proposal in the Simple Chat
dashboard.

## Privacy and data

Simple Chat returns only the data that a request needs. It removes card numbers from message text, and it does not
show the names of other staff members. Claude receives the conversation and order data that you ask for. The
[privacy policy](https://simple-chat.com/pages/privacy-policy) has the details under "AI Assistant Connectors".

## Disconnect

- In Simple Chat, open **Settings**, then **AI assistant connections**, and click **Revoke**.
- Or disconnect the connector in Claude.
- If you uninstall Simple Chat from the store, every connection stops.

## Support

Write to us from <https://simple-chat.com/pages/contact>. The
[terms of service](https://simple-chat.com/pages/terms-and-conditions) apply to the use of Simple Chat.
