---
layout: post
title:  "Hosting Red on Ubuntu using Docker"
date:   2023-06-18 20:40:00
categories: [Tutorials, Linux]
image: /assets/img/2023-06-18-red-discord-bot/red.png
tags: [linux, ubuntu, hosting, discord, discord bot]
---

## Red-DiscordBot: The Only Bot You'll Probably Need
This is Red-DiscordBot, the ultimate modular Discord bot that adapts to your preferences. With Red, you have full control over the features and commands you enable or disable, allowing you to create a customized bot experience tailored to your needs. From administration and music to trivia and more, Red has got your tail covered!

If you want to delve deeper into the world of Red, make sure to visit the <a href="https://github.com/Cog-Creators/Red-DiscordBot" target="_blank">Red-DiscordBot</a> repo for comprehensive information and resources.

## Red on Docker? Absolutely!
Thanks to the incredible work by <a href="https://github.com/PhasecoreX" target="_blank">PhasecoreX</a>, you can now harness the power of Red with ease using Docker. The <a href="https://github.com/PhasecoreX/docker-red-discordbot" target="_blank">docker-red-discordbot</a> repository provides everything you need to get started.

Here's why this Docker image stands out from the crowd:

- Runs securely without root privileges: Specify the user you want the bot to run as, ensuring maximum security and control.
- Quick and effortless setup: With a single Docker command, your new bot will be ready to wag its tail and join your server, saving you time and effort.
- Stay up-to-date effortlessly: Red-DiscordBot and the Docker image automatically update to the latest release, ensuring you always have the latest features.
- Compatible with various server architectures: Whether you're using a standard x86-64 server or arm(64) devices like Raspberry Pi, Red-DiscordBot has you covered.
- Stay informed with update notifications: The Docker image integrates with UpdateNotify, providing you with timely notifications for Red-DiscordBot and Docker image updates.
- Lightweight and efficient: The image size has been optimized to include only the essentials for running Red-DiscordBot and a vast majority of 3rd party cogs.

## Let's Get Started
Before you can host a Red bot, make sure you have the following:
- A server to host the bot (any host with a decent internet connection will do, and if you're looking for a personal recommendation, I typically use <a href="https://aws.amazon.com/lightsail/" target="_blank">AWS Lightsail</a>).
- A Discord Bot Token obtained by creating an Application on the <a href="https://discord.com/developers" target="_blank">Discord Developer Portal</a>.

> If you're a new Lightsail customer, you can get the $10 tier free for three months!
{: .prompt-tip }

## Obtaining a Bot Token
To get started, follow these simple steps to obtain your Discord Bot Token:

1. Head over to the <a href="https://discord.com/developers/applications" target="_blank">Discord Developer Portal</a>.
 - Click on New Application.
 - Give your app a name and accept the Developer Terms of Service and Developer Policy.
2. Navigate to the Bot section.
 - If you're satisfied with your bot's name, leave the Username as is.
 - Under Token, click Reset Token — this is the only chance to obtain your token.
 - Save the token as you won't be able to retrieve it later from this page.
 - Scroll down and ensure that Presence Intent, Server Members Intent, and Message Content Intent are all enabled.

## Deploying Red with Docker
To quickly deploy Red using Docker, use the following command:

```bash
docker run -v /local_folder_for_persistence:/data -e TOKEN=bot_token -e PREFIX=. phasecorex/red-discordbot
```

> Before running this command, make sure to replace the environment variables with the requested information.
{: .prompt-warning }

Variables:

- `-v /local_folder_for_persistence:/data`: Folder to store persistent data for Red. You can also use a named volume.
- `-e TOKEN=bot_token`: The token of the bot that was retrieved earlier.
- `-e PREFIX=.`: The prefix you'd like Red to use. By default, this is `.`. You can specify multiple prefixes by adding more variables, such as PREFIX2, PREFIX3, up to PREFIX5.

During the initial run, the container may take some time to start while all the Red dependencies are being installed. Subsequent starts should be much faster, like a lightning-fast tail wag.

> Want to monitor the installation progress or view logs? Use `docker logs --follow [containerid]` to see real-time logs.
{: .prompt-info }

More variables and what they do can be found on the <a href="https://github.com/PhasecoreX/docker-red-discordbot" target="_blank">GitHub Repo</a>.

## Docker Recommendations
Once your Red bot is up and running, you might want to give the container a meaningful name and configure it to restart with the system. The previous command only started the container with a random name. Use docker ps to view a list of running containers and their names.

Run the following commands to manage your container effectively:

```bash
# Stop the running container.
docker stop [containerID]

# Delete the container (data is retained unless you delete the persistence folder).
docker rm [containerID]

# Re-run the command with added variables.
docker run -v /local_folder_for_persistence:/data -d --name Friendly_Name --restart unless-stopped phasecorex/red-discordbot
```

> Replace `Friendly_Name` with the desired name for your bot or any address you prefer for the container.
{: .prompt-info }

Now you can use the Friendly_Name with any Docker command instead of needing to obtain the container ID, making management easier.

## Conclusion
By following the steps outlined above, you now have a running instance of Red-DiscordBot! To obtain the Invite link and invite the bot to your server, you may need to view the logs.

Remember to refer to the GitHub page for the Docker image to access additional information that wasn't covered here. Enjoy your Red-DiscordBot journey!