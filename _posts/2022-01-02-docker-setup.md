---
layout: post
title: "Bot setup (Docker)"
permalink: /setup/docker
---

* Table of Contents Placeholder
{:toc}

## Initial setup

First, you'll need Docker Engine and Docker Compose installed on your system. Once you have Docker and Compose set up, download the [sample Compose file](https://raw.githubusercontent.com/fluid-queue/fluid-queue/main/docker-compose.sample.yml) and save it to your root folder as `docker-compose.yml`. At the time of writing, this file does need a little modification, but once we're out of beta this file should work as-is if you're following along exactly.

Edit the Compose file and make sure the tag is set correctly (at the time of writing, this would be `fluidqueue/fluid-queue:2.0.0-beta.1` or `fluidqueue/fluid-queue:develop` if you're daring) and your volumes are set up correctly. If you've been following along exactly, your volumes should already be set up correctly: you should have a `docker-compose.yml`, `settings` folder, and `data` folder all within your root folder.

Next, follow the steps in [Configuring the bot](/configuring) and then come back here, we're not done yet!

## Important note

Once you've got your configuration done, you might need to make sure your folder permissions are corect. Docker uses the permisions from your filesystem, which may not line up with the state inside the Docker container: the bot runs as UID 1000 in Docker, which means that UID 1000 needs to be able to access the files in your `settings` and `data` directories. The easiest way to ensure this is with a quick `chmod -R go+rw data/ settings/` from your root directory.

And with that out of the way, you can move on to [Using the bot](/using)!

## Updates

Updates can be performed as usual with Docker: stop the bot (`docker compose down`), pull your tag (`docker compose pull`), then start the bot again (`docker compose up -d`). If you're on a specific version tag (like `fluidqueue/fluid-queue:2.0.0-beta.1`) make sure you switch tags first!

## Tags

We have a few autobuilds set up, as detailed in the following table:

| Tag                                        | Rule                                                 | Description                                                                                                         |
|--------------------------------------------|------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| latest                                     | Every push to `main`                                 | The latest stable updates.                                                                                          |
| develop                                    | Every push to `develop`                              | The bleeding-edge. May not be as stable, but will always be up to date.                                             |
| release-*                                  | Every manually tagged stable release (`v1.2.3`, etc) | Specific stable versions.                                                                                           |
| 2.0.0-beta.1<br>(and similar version tags) | Every manually tagged prerelease.                    | Specific alpha/beta/prerelease versions. Tagged on git as just the version number, rather than with a prefixed `v`. |

In general (and once we've done a proper full release), we would recommend tracking `latest`, however we try to keep `develop` stable as well.
