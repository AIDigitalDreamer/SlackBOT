# SlackBOT

I made this Slack bot using Node.js, `@slack/bolt`, and `axios` because I wanted a bot that could reply to slash commands 24/7 without me having to keep my laptop open all day. To make it run non-stop, I hosted it on my Hack Club Nest server.

## How to use the bot

Open the Hack Club Slack (like in `#bot-spam`) and type any of these slash commands:

- `/comsic-help` - Shows the list of available commands
- `/comsic-ping` - Checks if the bot is online and replies with `Pong!` and the latency in ms
- `/comsic-catfact` - Fetches and replies with a random cat fact
- `/comsic-joke` - Fetches and replies with a random joke and punchline

*(Note: Make sure to spell the command prefix `/comsic-` with the "m" before the "s"!)*

## Features

- Connects using Slack Socket Mode so it does not need a public HTTP endpoint.
- Uses `axios` to fetch live data from the Cat Fact API (`catfact.ninja`) and the Official Joke API.
- Calculates live response latency with `/comsic-ping`.
- Runs 24/7 in the background on Ubuntu using a Linux `systemd` service.

## How I made it

I started by setting up a Slack app on the Slack API website, turning on Socket Mode, creating the slash commands, and getting my bot and app tokens. I wrote the bot code in `index.js` using `@slack/bolt` and `axios`, and kept my tokens safe inside a `.env` file so they wouldn't get leaked on GitHub.

Moving the bot to the Hack Club Nest server took a lot of trial and error since I was new to using a Linux terminal. At first I tried connecting through SSH with the local IPv4 address and it kept timing out, so I had to figure out how to connect using the server's public IPv6 address instead.

Once I logged into the server, I installed Git and Node.js and cloned my repo. When I tried running `npm install`, it gave me an error because I forgot to upload my `package.json` file to GitHub. I went back to the GitHub website, added `package.json` manually, and ran `git pull` on the server to fix it. Then I used `nano` in the terminal to create my `.env` file and paste my tokens in.

At first I ran the bot with `node index.js`, which worked, but the bot turned off whenever I closed my SSH window. To fix that, I learned how to make a `slackbot.service` file in `/etc/systemd/system/` and started it with `systemctl`. Now the server keeps the bot running in the background 24/7 and restarts it automatically if it ever crashes.

## How to run it yourself

1. Clone this repository:
   `git clone https://github.com/AlDigitalDreamer/SlackBOT.git`
2. Install the packages:
   `npm install`
3. Create a `.env` file in the main folder and add your tokens:
   `SLACK_BOT_TOKEN=xoxb-your-token`
   `SLACK_APP_TOKEN=xapp-your-token`
4. Start the bot:
   `node index.js`
