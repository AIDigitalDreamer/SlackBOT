# My 24/7 Slack Bot (Hosted on Hack Club Nest!)

Hey there! I built this custom Slack bot for my Stardance project. I mainly wanted to figure out how to keep a coding project running permanently on a server, so I wouldn't have to keep my personal laptop awake all day just to host it. I wrote it in Node.js and hosted it on a Hack Club Nest Linux container.

## What it actually does
* **Always Awake:** It runs 24/7 in the background of my Nest server, so it never misses a message.
* **Instant Replies:** It listens for my custom slash commands in Slack and replies instantly.
* **Socket Mode:** It uses Slack's Socket Mode, meaning it connects securely without needing a public web server setup.

## How I built it (and the stuff that went wrong)
This was my first time really diving into a Linux command line, so it was a huge learning curve. I used the `@slack/bolt` framework for the bot's brain.

Here are the main challenges I ran into:
* **The Server Connection:** Getting onto the Nest server in the first place was tricky. I kept getting connection timeouts with the IPv4 address until I figured out how to SSH in using the server's public IPv6 address.
* **The `package.json` disaster:** When I finally got my code onto the server and tried to run `npm install`, it failed completely. I realized I had totally forgotten to commit and push my `package.json` file! I had to quickly write it up in the GitHub web interface and pull it back down to the server to fix it.
* **Going 24/7:** To stop the bot from dying the second I closed my terminal window, I had to learn about Linux background processes. I wrote a `systemd` service file (`slackbot.service`) to manage it. Seeing the terminal print `active (running)` for the first time was the best feeling!

## Want to run it yourself?
If you want to clone this and try it, you'll need Node.js installed and your own Slack App tokens from the Slack API dashboard.

1. Clone this repo and run `npm install` (I double-checked that `package.json` is actually there this time!).
2. Create a `.env` file in the folder and add your tokens like this:
   ```env
   SLACK_BOT_TOKEN=xoxb-your-bot-token
   SLACK_APP_TOKEN=xapp-your-app-token
   ```
3. Run `node index.js`. Once it says "bot is running!", test your slash command in Slack.
