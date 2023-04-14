---
layout: post
title: "Bot setup (Native)"
permalink: /setup/native
---

* Table of Contents Placeholder
{:toc}

## Setup

To run the bot natively, you'll need a recent version of [Node.JS](https://nodejs.org/en) installed. Our minimum supported version is Node 16, however we recommend you install the latest LTS release. (In case you were wondering, our Docker builds are based on Node 19 at time of writing, and we run tests on Node 16, 18, and 19.)

Once you have Node installed, head on over to our [Releases](https://github.com/fluid-queue/fluid-queue/releases) page and download the latest release. You can also clone the repository with `git clone https://github.com/fluid-queue/fluid-queue`; this makes it a little easier to update, or to switch over to our develop branch, but most users should be fine downloading the releases manually. (Note that if you already have a root folder set up with a `settings` and `data` directory within, you may not be able to clone directly to that folder; easily fixable by temporaily renaming it and then moving the contents over.)

If you downloaded the latest release, extract its contents to your root folder, making sure that "package.json" is directly within your root folder (in the same folder as your `settings` and `data` folders).

With the source code now extracted to your root folder, you're ready to configure the bot! Within the `settings` directory should now be two new files, "settings.example.json" and "tokens.example.json". Copy both those files, removing the "example" from their names, to `settings.json` and `tokens.json`. Now go over to the [configuration](/configuration) section to configure them!

## Updates

Updating the bot should be as simple as downloading the new release and extracting the files to your root directory again. If you're pulling directly from git, there may be additional instructions documented in CONTRIBUTING.md to build the bot.