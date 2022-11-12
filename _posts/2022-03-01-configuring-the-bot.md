---
layout: post
title: "Configuring the Bot"
permalink: /configuration
---

The settings.json file contains several options to make the bot as customizable as possible.

`username` is the username of your bot account or your account.

`password` is the oauth token of the bot, including the portion that says 'oauth'. This can be generated at https://twitchapps.com/tmi/.

`channel` is the channel that the bot will run in. This should be your Twitch account username, only containing underscores and lowercase alphanumeric characters.

`start_open` is the toggle for whether or not the queue will start open. The default value is `false`.

`enable_absolute_position` is the toggle for whether or not absolute position (offline position) is displayed along relative position (online position). The default value is `false`.

`custom_codes_enabled` is the toggle for whether or not custom codes are allowed to be added to the queue. When enabled, users are able to add an alias to the queue as opposed to the real ID. An example of this is `!add Kamek`. Before usage, the broadcaster must add custom codes to be used. This is detailed in the commands section.

`romhacks_enabled` is a toggle for whether or not romhacks are allowed to be added to the queue. When enabled, users may type `!add ROMhack` to add a ROMhack to the queue. This does not send the patch, but rather gives the user a convienent way to enter the queue without a real level code. It is required for `custom_codes_enabled` to be toggled on to use this feature, and the ROMhack code is added/removed automatically from the custom codes list depending on this toggle.

`max_size` is the maximum amount of levels allowed in the queue at once. The default value is `100`.

`level_timeout` is the amount of time in minutes a level can be played before the bot will inform you that time is up. The default value of `null` means that the timer is deactivated.

`level_selection` is an array that defines the order that levels will be selected in upon using `!level`. Once the order is completed, it will loop.
Possible values are: `"next"`, `"subnext"`, `"modnext"`, `"random"`, `"weightedrandom"`, `"weightednext"`, `"subrandom"`, `"modrandom"`, `"weightedsubrandom"`, and `"weightedsubnext"`

`message_cooldown` is the amount of time in seconds that a user must wait before !list will display the levels in the queue after a previous use. 

`dataIdCourseThreshold` is the highest allowed data ID for course IDs. This is used to stop levels that do not exist from entering the queue, however it is very difficult to know and/or dynamically change this amount accordingly. As such, the default value is `null`, which ignores the restriction.

`dataIdMakerThreshold` is the highest allowed data ID for maker IDs. This is used to stop maker IDs that do not exist from entering the queue, however it is very difficult to know and/or dynamically change this amount accordingly. As such, the default value is `null`, which ignores the restriction.

`prettySaveFiles` if set to true the files in the `./data/` directory are going to be formatted with spaces and new lines. The default value is `false` to reduce file size.

`subscriberWeightMultiplier` is the number added as a wait time for subscribers. The default value is `1.0`. Setting this to `1.2` for example will give subscribers an advantage for weighted random, because they would get 6 minutes of wait time per 5 minutes of waiting. This can be set to anything greater than or equal to `1.0`.

`list` is the order of the `!list`/`!queue` command. The following values are possible:
- `"position"` - the list will be sorted by time added. (`!next`)
- `"weight"` - the list will be sorted by weighted chance (watch time, `!weightednext`).
- `"both"` - the list will be sent twice, once sorted by time added and once sorted by weighted chance (watch time).
- `"none"` - the `!list`/`!queue` commands will be disabled.
- `null` - the setting is automatically determined by what is configured in `level_selection`.

`position` is which position the `!position` command shows. The following values are possible:
- `"position"` - the position of `!next`.
- `"weight"` - the position of `!weightednext`.
- `"both"` - both the position of `!next` and `!weightednext`.
- `"none"` - the `!position` command will be disabled.
- `null` - the setting is automatically determined by what is configured in `level_selection`.

`showMakerCode` if set to true it will display `(maker code)` next to level codes in chat if the code is a maker code. The default value is `true`.
