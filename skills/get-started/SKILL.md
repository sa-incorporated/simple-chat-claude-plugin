---
name: get-started
description: Check the Simple Chat connection, name the connected Shopify store, and show what to ask. Use when the user has just added Simple Chat, asks how to get started or what Simple Chat can do here, or when a Simple Chat tool is missing or fails because the connector is not connected.
---

# Get started with Simple Chat

Simple Chat is the support inbox and AI agent of a Shopify store. The connector acts as the staff member who connected
it, on one store only.

1. Check the connection by calling `list_inbox_conversations` with `{}`.
   - If the Simple Chat tools are missing, or the call fails because nobody is signed in, tell the user to connect the
     Simple Chat connector, and stop. On claude.ai and in the desktop app, they connect it on the plugin's Connectors
     tab. In Claude Code, they run `/mcp`, choose the Simple Chat server and sign in.
   - Sign-in asks for the store's `myshopify.com` address, then for approval in that store's Shopify admin. The store
     needs Simple Chat installed from the Shopify App Store.
2. Name the connected store. The server's instructions say which store this connection reached ("Connected to Simple
   Chat for the store …"). Say it in one short sentence, and mention how many conversations are waiting, if any.
3. Offer three things they can ask, one line each:
   - "What's waiting for me in Simple Chat?"
   - "Show the drafts and proposals that need my approval"
   - "Why is AI resolution low for Returns and refunds? Replay it for the last 90 days."
4. Explain in three sentences. First: sending or discarding a drafted customer reply, approving an order change or a
   customer record card, rejecting a proposal card, and running a paid topic replay only happen after they click
   Confirm in the card that appears. Second: a refund, an order cancel and a replacement order are approved in the
   Simple Chat dashboard and not from Claude, and topic replay needs the Premium plan. Third: a change of an FAQ or of
   the store instructions of the AI applies at once when they ask for it.

Keep it short. If the user added the plugin in the middle of a task, continue that task in the same conversation.
Never quote customer messages back during setup.
