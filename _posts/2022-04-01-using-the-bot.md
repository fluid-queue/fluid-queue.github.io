---
layout: post
title: "Using the bot"
permalink: /using
---

* Table of Contents Placeholder
{:toc}

## Running the bot

To use the bot, you'll need to start it.

### Docker

Depending on how your system is set up, you'll need to use either `docker compose` or `docker-compose`. For either, you can start the bot like this to make sure it works and doesn't give you any errors:

`docker compose up`

Once it's running (or if it's giving you a bunch of errors), press Control+C to stop it. If everything's good, you can now run it in detached mode:

`docker compose up -d`

To stop the bot in detached mode, you can use `docker compse down`.

### Native

To run the bot natively, just run:

`npm run start`

and use Control+C to stop the bot.

## Bot Operation

### Chat commands

The following list contains all commands and aliases accessible by default to you while using the queue. All commands marked with **[!]** are only accessible to the channel owner.

It is important to note that all commands that draw a level (with exception to `!dismiss`) will first remove the currently selected level before drawing a new one.

- `!open` opens the queue and allows levels to be added. **[!]**
- `!close` closes the queue and prevents levels from being added. **[!]**
- `!clear` will remove all levels from the queue, including the current level. **[!]**
- `!add` adds a level or maker ID to the queue, provided a level code or maker ID follows the command.
- `!remove`/`!leave` will remove a user's submitted level or maker ID from the queue. If used by the channel owner, a name can be specified to remove another user's level or maker ID.
- `!replace`/`!change`/`!swap` will swap a user's level code for the one following the command. Queue position is preserved when this is used.
- `!brb` will mark the user as offline. Their levels cannot be selected while in this state.
- `!back` will mark the user as online. Their levels can be selected while in this state.
- `!current` will show the currently selected level or maker ID as well as who submitted it.
- `!order` will show the level selection order as defined in the settings.js file. It also shows what the next level selection will be.
-`!list`/`!queue` will show an in-order list of levels in the queue. It will display the current level as well as the next 5 levels of those currently online. It will also display how many people in the queue are offline.
- `!position` will output the user's position in the queue, provided they have one.
- `!submitted`/`!entry`/`!mylevel`/`!mylvl` will output the user's submitted level code, provided they have submitted a level.
- `!weightedchance`/`!odds`/`!chance`/`!chances` will output the user's chances of getting selected in weighted random.
- `!level` will select a level from the queue with respect to the order defined in the settings.js file. **[!]**
- `!next` will select the next level from the queue. **[!]**
- `!random` will select a random level from the queue. **[!]**
- `!weightedrandom` will select a random level from the queue using the amount of time spent online and waiting in the queue as weight. **[!]**
- `!weightednext` will select the level from the queue with the most amount of time spent online and waiting in the queue. If multiple users have the same maximum time spent then the level nearer to the top will be chosen. **[!]**
- `!subnext` will select the next subscriber's level from the queue. **[!]**
- `!subrandom` will select a random subscriber's level from the queue. **[!]**
- `!weightedsubrandom` will select a random level from the subscribers using the amount of time spent online and waiting in the queue as weight. **[!]**
- `!weightedsubnext` will select the level from the queue with the most amount of time spent online and waiting in the queue and being subscribed. If multiple users have the same maximum time spent then the level nearer to the top will be chosen. **[!]**
- `!modnext` will select the next moderator's level from the queue. **[!]**
- `!modrandom` will select a random moderator's level from the queue. **[!]**
- `!dismiss`/`!skip`/`!complete`/`!completed` will remove the current level from the queue without drawing a new one. **[!]**
- `!select` will select a specific user's level, provided it is defined after the command. **[!]**
- `!punt` will move the currently selected level to the back of the queue. **[!]**
- `!customcodes` will display all of the custom codes that are set, provided the feature is enabled. If this is used by the broadcaster, it can also be used to add and remove custom codes. The appropriate syntax for this is `!customcode {add/remove/load} {customCode} {ID}` where `add`/`remove`/`load` is the desired operation, customCode is the custom code that the user would like to type (example being `!add Kamek`), and ID being the ID that the custom code is an alias of. If a code is being removed, the ID is not required. Please note that while adding or removing the custom codes from the _queue_ are not case sensitive, they are case sensitive with this command.
  - `!customcode load` will reload the custom codes from the `./customCodes.json` file, so you can manually edit that file and then reload the codes without having to restart the queue.
- `!customlevels` will display all of the custom levels including their custom codes.
- `!persistence` will give control over how and if the queue data is loaded/saved: **[!]**
  - `!persistence save` will manually save the queue state (current level, queue, wait time) to `./data/queue.json`.
  - `!persistence on` will set the queue to automatically save its state whenever changes occur. (this is the default behaviour)
  - `!persistence off` will deactivate any changes to be saved.
  - `!persistence load` will manually load the queue state (current level, queue, wait time) from `./data/queue.json`. Please use this with caution since reloading the state can result in lost data and it is recommended to:
    - use `!persistence off` to prevent the queue from overriding changes you are going to make
    - make changes to `./data/queue.json`
    - use `!persistence load` to load these changes
    - use `!persistence on` to reactivate automatic saves

### Custom Level Types

Custom level types are levels that have no level code associated.

For example one might play uncleared levels from time to time and while doing viewer levels a viewer might want to submit an uncleared level (`!add uncleared`), but does not want to add a specific uncleared level to the queue. When the level gets picked, there will be no code and the streamer only sees that an uncleared level was picked and then the streamer may pick an uncleared level on their own.

Some more examples would be to be able to submit a maker team level (like team shell, team jamp or team precision) without submitting a specific level code, or to be able to submit a no skip super expert run etc. This could also be used to submit maker 1 levels or could be used for other games in general by just having a custom level type for that game and when people get picked they could join that game for example etc.

#### Setting up custom level types

There are some build-in custom level types:

- **Uncleared levels**

  To enable uncleared levels make sure to set `uncleared_enabled` to `true` in `settings.json`.
  To add uncleared levels use:
  `!add Uncleared`, or any of the alternatives: `!add UNC-LEA-RED`, `!add an uncleared level`, `!add uncleared level`

- **ROMhacks**

  To enable ROMhacks make sure to set `romhacks_enabled` to `true` in `settings.json`.
  To add ROMhacks use:
  `!add ROMhack`, or any of the alternatives: `!add R0M-HAK-LVL`, `!add rom hack`

You can also add your own custom levels:

`!customlevel add {customCode} {levelName...}`

where `customCode` will be a custom code how you will add this custom level with `!add {customCode}` and `levelName...` can be multiple words to describe the custom level.

For example the level name of an uncleared level is `an uncleared level`.
The level name will appear in sentences like these:

- `Currently playing {levelName...} submitted by {user}.`
- `{user}, you have submitted {levelName...} to the queue.`
- `{user}, {levelName...} has been added to the queue.`
- `{user}, your level in the queue has been replaced with {levelName...}.`

For example you could use this command to be able to add team shell levels to the queue: `!customlevel add teamshell a team shell level`
and when someone uses `!add teamshell` then the bot will respond with `[...], a team shell level has been added to the queue.`.

#### Removing custom level types

To remove ROMhacks you would need to set `romhacks_enabled` to `false` and to remove uncleared levels you would need to set `uncleared_enabled` to `false`.

The custom level type is added/removed automatically from the custom level types list in `./data/queue.json` depending on the configuration. If the configuration is set to `false`, but there are still levels in the queue, then they will still show up and are still saved to the json file, however no new levels can be added to the queue. Whenever all levels are removed from the queue (e.g. by them getting picked or by using `!clear` to remove all levels from the queue) and the configuration is set to `false` then the custom level type is removed from the save file.

To remove other custom levels use the following command:

`!customlevel remove {customCode}`

E.g. `!cusomlevel remove teamshell`

To disable custom levels instead use:

`!customlevel disable {customCode}`

Disabling custom levels will make them not submittable, but levels that are still present in the queue will still be displayed correctly.

To enable custom levels again use:

`!customlevel enable {customCode}`

You can add more codes to a custom level with:

`!customlevel code add {newCode} {customCode}`

And also remove codes with:

`!customlevel code remove {customCode}`

#### Importing/Exporting custom level types

To make sharing and installing custom level types easier the queue has an import and export function.

`!customlevel export {customCode}`

`!customlevel import {json}`

For example:

```
!customlevel add teamshell a team shell level
Created custom level "a team shell level" with code teamshell.
!customlevel code add TS teamshell
Added the code TS to the custom level with the name "a team shell level" and codes teamshell, TS.
!customlevel export TS
["d762ea56-cb01-4215-9e9c-1c4e7626da3f","a team shell level","teamshell","TS"]
```

Now someone else can just import that custom level:

```
!customlevel import ["d762ea56-cb01-4215-9e9c-1c4e7626da3f","a team shell level","teamshell","TS"]
Created custom level "a team shell level" with codes teamshell, TS.
```

### Aliases

The following list of commands are available to manage aliases:

`!aliases` will display the available aliases management commands and the available commands you can put aliases for.

- `!addalias command alias` adds the alias `alias` for command `command`
- `!removealias command alias` removes the alias `alias` for command `command`
- `!enablecmd command` enables the command `command`
- `!disablecmd command` disables the command `command` entirely.
- `!resetcmd command` resets the command `command` to default values.

The aliases are saved in a file in `./settings/aliases.json`. Please use this with caution. It might render the bot inoperable.