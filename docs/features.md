## Card Restore

If active, FlipperMCE will always boot to the last used card.

## Game ID

Many loaders implement a special protocol, that allows the cube to transmit the Game ID of the currently started game to an *MCE*.

FlipperMCE supports this protocol (see *doc/mcp*) and will load or create a card for each trasmitted Game ID if configured so.

As a bonus, it will select the correct default card encoding for the game.

## Mulitple CardSizes

*FlipperMCE* support Card Sizes from 4 - 64 MBits.

Since the naming scheme for cards is confusing, please see following explanation:

| MBit    | Blocks    | Size (MB) |
|---------|-----------|-----------|
| 4       | 59        | 0.5       |
| 8       | 123       | 1         |
| 16      | 251       | 2         |
| 32      | 507       | 4         |
| 64      | 1019      | 8         |

## Game2Folder mapping

There are some games, that share save data for multiple game ids. For these cases, a custom game to folder mapping can be created.

If a game with a mapped id is loaded, instead of using the game id based folder, the mapped folder is used for storing the card.

The mapping needs to be defined in ```.flippermce/Game2Folder.ini``` in the following way:

```ini
[GC]
GT4P=FolderName
```

*Note: Make sure there is an empty line at the end of the ini file.*


## Settings File

*FlipperMCE* generates a settings file (`.flippermce/settings.ini`) that allows you to edit some settings through your computer. This is useful when using one SD card with multiple *FlipperMCE* devices.

A settings file has the following format:

```ini
[General]
FlippedScreen=OFF
[GC]
CardRestore=ON
GameID=ON
CardSize=64
```

Possible values are:

| Setting       | Values                      | Description                  |
|---------------|-----------------------------|------------------------------|
| CardRestore   | `OFF`, `ON`                 | Restore last card at boot    |
| GameID        | `OFF`, `ON`                 | Use Game ID if transmitted   |
| CardSize      | `4`, `8`, `16`, `32`, `64`  | Default CardSize in MBit     |
| FlippedScreen | `ON`, `OFF`                 | Flip the screen horizontally |

*Note: Make sure there is an empty line at the end of the ini file.*

## Per Card Configs

There are some configuration values that can be modified on a per card base within a config file named  `CardX.ini` in a card folder, where `X` is the card index.

*Note: Make sure there is an empty line at the end of the ini file.*

```ini
[ChannelName]
1=Channel 1 Name
2=Channel 2 Name
3=Channel 3 Name
4=Channel 4 Name
5=Channel 5 Name
6=Channel 6 Name
7=Channel 7 Name
8=Channel 8 Name
[Settings]
MaxChannels=8
CardSize=4
```
