# My 24/7 Nest Slack Bot 🚀

Hey! I'm Kavish, and this is my Stardance software project. I built a custom Slack bot using Node.js and the `@slack/bolt` library. The main goal for this project was figuring out how to host a bot 24/7 on a Hack Club Nest server so I wouldn't have to leave my personal laptop running all day.

## How to interact with the bot
If you are in the Slack workspace where my bot is installed, here is how you can test it:
1. Go to a channel like `#bot-spam` (or wherever it is added).
2. Type my custom slash command: `/your-command-here` 
3. Hit enter! Because the bot is running 24/7 on my Nest container using Socket Mode, it will reply to you instantly.

## My Coding Journey (and the things I broke)
I had never really used a Linux server command line before this, so getting it to run permanently was a massive learning experience.

* **Getting into the server:** I spent a long time trying to SSH into my Nest container with the standard IPv4 address, and it kept timing out. I finally figured out I needed to use the public IPv6 address to connect.
* **The package.json mistake:** After I got into the server and cloned my GitHub repo, I proudly ran `npm install`... and it immediately crashed. I realized I had completely forgotten to upload my `package.json` file to GitHub. I had to create the file directly in the GitHub web UI and run `git pull` on the server to fix it.
* **Keeping it alive:** Initially, whenever I closed my SSH terminal, the bot would die. I had to research Linux background processes and wrote my very first `systemd` service script (`slackbot.service`). Once I got the `active (running)` status, it stayed online for good.

## Running the code yourself
If you want to host this on your own machine:
1. Clone this repository.
2. Run `npm install` (I made sure the `package.json` is actually there this time!).
3. Create a `.env` file and add your own Slack App credentials:
   ```env
   SLACK_BOT_TOKEN=xoxb-your-bot-token
   SLACK_APP_TOKEN=xapp-your-app-token
   ```
4. Run `node index.js`.
