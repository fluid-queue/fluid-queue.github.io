---
layout: post
title: "Bot Commands"
permalink: /commands
---

The following list contains all commands and aliases accessible to you while using the queue. All commands marked with an asterisk are only accessible to the channel owner.

It is important to note that all commands that draw a level (with exception to `!dismiss`) will first remove the currently selected level before drawing a new one.

`!open`* opens the queue and allows levels to be added.

`!close`* closes the queue and prevents levels from being added.

`!clear`* will remove all levels from the queue, including the current level.

`!add` adds a level or maker ID to the queue, provided a level code or maker ID follows the command.

`!remove`/`!leave` will remove a user's submitted level or maker ID from the queue. If used by the channel owner, a name can be specified to remove another user's level or maker ID.

`!replace`/`!change`/`!swap` will swap a user's level code for the one following the command. Queue position is preserved when this is used.

`!brb` will mark the user as offline. Their levels cannot be selected while in this state.

`!back` will mark the user as online. Their levels can be selected while in this state.

`!current` will show the currently selected level or maker ID as well as who submitted it.

`!order` will show the level selection order as defined in the settings.js file. It also shows what the next level selection will be.

`!list`/`!queue` will show an in-order list of levels in the queue. It will display the current level as well as the next 5 levels of those currently online. It will also display how many people in the queue are offline.

`!position` will output the user's position in the queue, provided they have one.

`!submitted`/`!entry`/`!mylevel`/`!mylvl` will output the user's submitted level code, provided they have submitted a level.

`!weightedchance`/`!odds`/`!chance`/`!chances` will output the user's chances of getting selected in weighted random.

`!level`* will select a level from the queue with respect to the order defined in the settings.js file.

`!next`* will select the next level from the queue.

`!random`* will select a random level from the queue.

`!weightedrandom`* will select a random level from the queue using the amount of time spent online and waiting in the queue as weight.

`!weightednext`* will select the level from the queue with the most amount of time spent online and waiting in the queue. If multiple users have the same maximum time spent then the level nearer to the top will be chosen.

`!subnext`* will select the next subscriber's level from the queue.

`!subrandom`* will select a random subscriber's level from the queue.

`!weightedsubrandom`* will select a random level from the subscribers using the amount of time spent online and waiting in the queue as weight.

`!weightedsubnext`* will select the level from the queue with the most amount of time spent online and waiting in the queue and being subscribed. If multiple users have the same maximum time spent then the level nearer to the top will be chosen.

`!modnext`* will select the next moderator's level from the queue.

`!modrandom`* will select a random moderator's level from the queue.

`!dismiss`/`!skip`/`!complete`* will remove the current level from the queue without drawing a new one.

`!select`* will select a specific user's level, provided it is defined after the command.

`!punt`* will move the currently selected level to the back of the queue.

`!customcodes` will display all of the custom codes that are set, provided the feature is enabled. If this is used by the broadcaster, it can also be used to add and remove custom codes. The appropriate syntax for this is `!customcode {add/remove/load} {customCode} {ID}` where `add`/`remove`/`load` is the desired operation, customCode is the custom code that the user would like to type (example being `!add Kamek`), and ID being the ID that the custom code is an alias of. If a code is being removed, the ID is not required. Please note that while adding or removing the custom codes from the *queue* are not case sensitive, they are case sensitive with this command.
`!customcode load` will reload the custom codes from the `./customCodes.json` file, so you can manually edit that file and then reload the codes without having to restart the queue.

`!persistence` * will give control over how and if the queue data is loaded/saved:
  - `!persistence save` will manually save the queue state (current level, queue, wait time) to `./data/queue.json`.
  - `!persistence on` will set the queue to automatically save its state whenever changes occur. (this is the default behaviour)
  - `!persistence off` will deactivate any changes to be saved.
  - `!persistence load` will manually load the queue state (current level, queue, wait time) from `./data/queue.json`. Please use this with caution since reloading the state can result in lost data and it is recommended to:
    - use `!persistence off` to prevent the queue from overriding changes you are going to make
    - make changes to `./data/queue.json`
    - use `!persistence load` to load these changes
    - use `!persistence on` to reactivate automatic saves