# Hack Club Slack Bot

A custom Slack bot built with Node.js and the `@slack/bolt` framework. This bot is configured to respond to slash commands via Socket Mode and is deployed to run 24/7 on a Hack Club Nest Linux server.

## Features
* Listens and responds to Slack slash commands natively.
* Built with the official Slack Bolt API for Node.js.
* Configured for continuous background deployment using `systemd` on Ubuntu.

## Prerequisites
* **Node.js** (v18 or higher recommended)
* A Slack Workspace where you have permission to create and install apps.
* Slack App Tokens (`SLACK_BOT_TOKEN` and `SLACK_APP_TOKEN`). Socket Mode must be enabled in your Slack API dashboard.

## Local Setup

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
   cd your-repo-name
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Configure environment variables:**
   Create a `.env` file in the root directory and add your Slack tokens. (Note: `.env` is ignored by git for security).
   ```env
   SLACK_BOT_TOKEN=xoxb-your-bot-token
   SLACK_APP_TOKEN=xapp-your-app-token
   ```

4. **Run the bot:**
   ```bash
   npm start
   ```
   *You should see "bot is running!" and "Now connected to Slack" in your console.*

## Deployment to Nest (Ubuntu)

This bot is configured to run as a continuous background service on a Nest container so it stays online 24/7.

1. SSH into your Nest server.
2. Clone the repository and run `npm install`.
3. Manually recreate your `.env` file on the server using `nano .env`.
4. Create a `systemd` service file at `/etc/systemd/system/slackbot.service`:
   ```ini
   [Unit]
   Description=Slack Bot
   After=network-online.target
   Wants=network-online.target

   [Service]
   Type=simple
   User=root
   Restart=always
   RestartSec=3
   WorkingDirectory=/root/SlackBOT
   ExecStart=/usr/bin/node index.js

   [Install]
   WantedBy=multi-user.target
   ```
5. Enable and start the background service:
   ```bash
   systemctl daemon-reload
   systemctl enable --now slackbot.service
   ```

## License
MIT
