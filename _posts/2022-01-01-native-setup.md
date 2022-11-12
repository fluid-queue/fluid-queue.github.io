---
layout: post
title: "Bot setup (Native)"
permalink: /native-setup
---

First, you need to get the bot's source code. Either download the latest release, or clone the repository with the following command:

```bash
$ git clone https://github.com/fluid-queue/fluid-queue
```

Next, install the dependencies for the project:

```bash
$ npm install
```

After that, copy and configure the `settings.json` file with your favorite text editor.

Further details on how to configure the bot can be found [here](/configuration).

```bash
$ cp settings.example.json settings.json
```

Finally, run the following command to start the bot:

```bash
$ npm run start
```

To close the queue press `CTRL + C` inside the terminal.

The command `npm run start` is the only command you will need to the next time you want to start the bot.

