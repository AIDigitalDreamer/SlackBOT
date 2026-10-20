# SlackBOT

I created this Slack bot with Node.js and @slack/bolt because I wanted a bot that would respond to messages around the clock, not requiring my laptop to be left opened all the time. To run it continuously, I hosted this bot on my Hack Club Nest server.

## How to use the bot

1. Access the Hack Club Slack and go to the `#bot-spam` channel.
2. Send a mention to `@SlackBOT` or type `hello`.
3. Receive a response to your message.

## Features

- Communicates via Slack Socket Mode thus no need for an exposed HTTP endpoint is required.
- Responds automatically to messages sent in the Slack.
- Operates 24/7 in the background via Ubuntu Linux systemd service.

## How I made it

To begin with, I created a Slack application on the Slack API website, activated Socket Mode, and received my bot token and app token. The code of the bot was written in `index.js` with `@slack/bolt`, while my tokens were stored in `.env` files to prevent their leaking to the GitHub.

Transferring the bot to the Hack Club Nest server was challenging due to the lack of experience in using a Linux terminal. Firstly, I tried to connect via SSH with the local IPv4 address and found out it always times out, so I had to find out how to connect with the IPv6 public address of the server instead.

Upon logging in, I had to install Git and Node.js and clone my repository. After attempting to run `npm install` and receiving the error, I found out that I had forgotten to upload `package.json` to GitHub. Therefore, I uploaded `package.json` via GitHub website and ran `git pull` on the server.

Next, I created `.env` file in the terminal using `nano` and pasted my tokens there.

Running the bot with `node index.js` was working fine; however, once I exited the SSH terminal, the bot was stopping. To solve this problem, I learned how to create a `slackbot.service` file in the `/etc/systemd/system/` directory and start it with `systemctl`.

Now, the server runs the bot 24/7 and restarts it in case of a crash.

## How to run it yourself

1. Clone this repository:
   `git clone https://github.com/AlDigitalDreamer/SlackBOT.git`
2. Install the packages:
   `npm install`
3. Create a `.env` file in the main folder and add your tokens:
   `SLACK_BOT_TOKEN=xoxb-your-token`
   `SLACK_APP_TOKEN=xapp-your-token`
4. Start the bot:
   `node
