# AI-Powered Slack Recipe Assistant (n8n & OpenAI)

An event-driven Slack bot built with **n8n**, **OAuth2**, and **OpenAI** that acts as an automated kitchen assistant. When a user requests a dish name in a dedicated Slack channel, the bot automatically generates a detailed, structured recipe and replies in real time.

---

## 🚀 How It Works

1. **User Request:** A user posts a dish name (e.g., *Paneer Butter Masala*) in the designated `#kitchen-assistant` channel[cite: 1].
2. **Event Capture:** An n8n **Slack Trigger** node listens to incoming channel events via Slack Event Subscriptions[cite: 1].
3. **Loop Prevention:** An internal filter checks for `bot_id` to ensure the bot's own replies do not trigger an infinite messaging loop.
4. **AI Generation:** An **OpenAI** model processes the requested dish and generates a comprehensive response including prep/cook times, ingredients, step-by-step instructions, chef's secrets, and substitutions[cite: 2].
5. **Automated Delivery:** A **Slack (Send a Message)** node posts the formatted recipe back to the exact originating channel[cite: 1, 2].

---

## 🛠️ Tech Stack & Tools

* **Automation Platform:** [n8n](https://n8n.io/) (Self-hosted or Cloud)
* **Messaging Platform:** Slack API (Custom App with OAuth2)
* **AI Model:** OpenAI GPT / Master Chef Model[cite: 2]

---

## 📋 Setup & Installation Instructions

### 1. Slack App Configuration
* Create a Slack App in the [Slack API Dashboard](https://api.slack.com/apps).
* Enable **OAuth & Permissions** and add the following **Bot Token Scopes**:
  * `chat:write`
  * `channels:read`
  * `groups:read`
  * `users:read`
* Install the app to your workspace using **OAuth2** and save your Client ID, Client Secret, and Redirect URL inside n8n.
* Enable **Event Subscriptions**, subscribe to the `message.channels` bot event, and paste your n8n Production Webhook URL as the Request URL.

### 2. n8n Workflow Import
* Import your n8n workflow JSON file into your n8n instance.
* Connect your **Slack OAuth2 Credential** and your **OpenAI Credential**.
* Ensure the **Slack Trigger** node points to your designated channel (e.g., `#kitchen-assistant`)[cite: 1].
* Toggle the workflow from **Inactive** to **Active**.

### 3. Testing
* Invite your bot to the channel (`/invite @Your_Bot_Name`)[cite: 1].
* Type any recipe name in the channel and watch your AI kitchen assistant reply instantly[cite: 1, 2]!