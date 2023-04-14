---
layout: post
title: "Configuring the Bot"
permalink: /configuration
---

* Table of Contents Placeholder
{:toc}

## `tokens.json`

`tokens.json` contains four mandatory fields:

- "accessToken" is the access token provided by Twitch CLI, or updated by the bot itself as necessary.
- "refreshToken" is the refresh token provided by Twitch CLI, or updated by the bot itself when it expires.
- "expiresIn" is set by the bot periodically, and should be set to 0 during initial setup.
- "obtainmentTimestamp" is also set by the bot periodically, and should be set to 0 during initial setup.

Please note that the braces in the example file are part of the placeholders; there should be **no braces** in your actual values. The braces at the start and end of the file are necessary.

Once this file is set up, you shouldn't need to worry about it again—though if you go for a while without using the bot, your access token may expire, and you'll need to manually authenticate with the Twitch CLI again. If that happens, just update your accessToken and refreshToken, set the other values to 0, and start the bot again.

## `settings.json`

`settings.json` is where most of the customization of the bot occurs. There's a lot of customization to do, and most of the options are safe to leave as the defaults, but there are a few to make sure you update, marked with **[!]** to make it easier to notice!

- **[!]** `channel` is the channel that the bot will run in. This should be your Twitch account username, only containing underscores and lowercase alphanumeric characters.
- **[!]** `clientId` is the client ID you received from Twitch when you registered your application. Again, don't include the braces.
- **[!]** `clientSecret` is the client secret you received from Twitch when you registered your application. No braces!
- `start_open` is the toggle for whether or not the queue will start open. The default value is `false`.
- `enable_absolute_position` is the toggle for whether or not absolute position (offline position) is displayed along relative position (online position). The default value is `false`.
- `custom_codes_enabled` is the toggle for whether or not custom codes are allowed to be added to the queue. When enabled, users are able to add an alias to the queue as opposed to the real ID. An example of this is `!add Kamek`. Before usage, the broadcaster must add custom codes to be used. This is detailed in the commands section.
  - If you enable custom codes, make sure to leave the custom code resolver enabled below!
- `romhacks_enabled` is a toggle for whether or not romhacks are allowed to be added to the queue. When enabled, users may type `!add ROMhack` to add a ROMhack to the queue. This does not send the patch, but rather gives the user a convienent way to enter the queue without a real level code. 
  - This requires the custom level resolver to be enabled below.
- `uncleared_enabled` is a similar toggle, for uncleared levels rather than than romhacks.
  - Again, you'll need to have the custom level resolver enabled for this to work.
- `max_size` is the maximum amount of levels allowed in the queue at once. The default value is `100`.
- `level_timeout` is the amount of time in minutes a level can be played before the bot will inform you that time is up. The default value of `null` means that the timer is deactivated.
-  `level_selection` is an array that defines the order that levels will be selected in upon using `!level`. Once the order is completed, it will loop.
  - Possible values are: 
    - `"next"`: select the next level in the queue with no preferences
    - `"subnext"`: select the next subscriber in the queue
    - `"modnext"`: select the next Twitch mod in the queue
    - `"random"`: select a random level with no preferences
    - `"weightedrandom"`: select a random level with no preferences, but weighted based on how long the viewer has been waiting
    - `"weightednext"`: select the viewer who has been waiting longest in the queue
    - `"subrandom"`: select a random subscriber in the queue
    - `"modrandom"`: select a random Twitch mod in the queue
    - `"weightedsubrandom"`: select a random subscriber, weighted based on how long the subscriber has been waiting
    - `"weightedsubnext"`: select the subscriber who has been waiting longest in the queue
- `message_cooldown` is the amount of time in seconds that a user must wait before !list will display the levels in the queue after a previous use. 
- `dataIdCourseThreshold` is the highest allowed data ID for course IDs. This is used to stop levels that do not exist from entering the queue, however it is very difficult to know and/or dynamically change this amount accordingly. As such, the default value is `null`, which ignores the restriction. This setting only applies to the `smm2` and `smm2-lenient` resolvers.
- `dataIdMakerThreshold` is the highest allowed data ID for maker IDs. This is used to stop maker IDs that do not exist from entering the queue, however it is very difficult to know and/or dynamically change this amount accordingly. As such, the default value is `null`, which ignores the restriction. This setting only applies to the `smm2` and `smm2-lenient` resolvers.
- `prettySaveFiles` if set to true the files in the `./data/` directory are going to be formatted with spaces and new lines. The default value is `false` to reduce file size.
- `subscriberWeightMultiplier` is the number added as a wait time for subscribers. The default value is `1.0`. Setting this to `1.2` for example will give subscribers an advantage for weighted random, because they would get 6 minutes of wait time per 5 minutes of waiting. This can be set to anything greater than or equal to `1.0`.
- `list` is the order of the `!list`/`!queue` command. The following values are possible:
  - `"position"` - the list will be sorted by time added. (`!next`)
  - `"weight"` - the list will be sorted by weighted chance (watch time, `!weightednext`).
  - `"both"` - the list will be sent twice, once sorted by time added and once sorted by weighted chance (watch time).
  - `"none"` - the `!list`/`!queue` commands will be disabled.
  - `null` - the setting is automatically determined by what is configured in `level_selection`.
- `position` is which position the `!position` command shows. The following values are possible:
  - `"position"` - the position of `!next`.
  - `"weight"` - the position of `!weightednext`.
  - `"both"` - both the position of `!next` and `!weightednext`.
  - `"none"` - the `!position` command will be disabled.
  - `null` - the setting is automatically determined by what is configured in `level_selection`.
- `showMakerCode` if set to true it will display `(maker code)` next to level codes in chat if the code is a maker code. The default value is `true`.
- **[!]** `resolvers` is the list of code resolvers to use to determine if a code is valid and allow it to be added to the queue. Valid resolvers are:
  - `smm2` and `smm2-lenient` for Super Mario Maker 2 codes
  - `ocw` and `ocw-lenient` for [Open Course World](https://opencourse.world) codes
  - `customcode` for custom codes, if enabled
  - `customlevel` and `customlevel-name` for custom levels, if enabled
  - `smm1` for Super Mario Maker 1 codes
  You can enable whichever of these you'd like in whichever order you'd like, however we recommend keeping them in the order presented in the sample file, and making sure that both resovlers are enabled for a given level type. This ensures the most accurate and responsive resolution of codes, while still giving viewers some leeway on their code format.

  ## Next steps

  Once you have the configuration complete and your `settings.json` and `tokens.json` saved in the `settings` folder, you're ready to start the bot. If you're using Docker, head back over to the [Docker instructions](/setup/docker) to read an important note about permissions, otherwise continue on to [Using the bot](/using).