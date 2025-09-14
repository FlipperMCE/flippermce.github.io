## FlipperMCE Features

This document describes the main features and configuration options available for FlipperMCE, including card restore, Game ID support, multiple card sizes, folder mapping, configuration files, and splash screen customization.

## Card Restore

When enabled, FlipperMCE will always boot to the last used card.

## Game ID

Many loaders implement a special protocol that allows the GameCube to transmit the Game ID of the currently started game to a Memory Card Emulator (MCE).

FlipperMCE supports this protocol (see the documentation in `doc/mcp`) and will load or create a card for each transmitted Game ID if configured to do so.

As a bonus, it will select the correct default card encoding for the game.

Game ID cards will reside in `MemoryCards/GC/<GameID>`.

## Multiple Card Sizes

FlipperMCE supports card sizes from 4 to 64 MBit.

Since the naming scheme for cards can be confusing, please see the following explanation:

| MBit | Blocks | Size (MB) |
|------|--------|-----------|
| 4    | 59     | 0.5       |
| 8    | 123    | 1         |
| 16   | 251    | 2         |
| 32   | 507    | 4         |
| 64   | 1019   | 8         |

## Game2Folder Mapping

Some games share save data for multiple Game IDs. For these cases, a custom game-to-folder mapping can be created.

If a game with a mapped ID is loaded, instead of using the Game ID-based folder, the mapped folder is used for storing the card.

The mapping needs to be defined in `.flippermce/Game2Folder.ini` as follows:

```ini
[GC]
GT4P=FolderName
```

In this case, *FolderName* refers to a folder located under `/MemoryCards/GC`.

*Note: Make sure there is an empty line at the end of the ini file.*

## Settings File

FlipperMCE generates a settings file (`.flippermce/settings.ini`) that allows you to edit some settings through your computer. This is useful when using one SD card with multiple FlipperMCE devices.

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

| Setting       | Values                     | Description                        |
|---------------|---------------------------|------------------------------------|
| CardRestore   | `OFF`, `ON`               | Restore last card at boot          |
| GameID        | `OFF`, `ON`               | Use Game ID if transmitted         |
| CardSize      | `4`, `8`, `16`, `32`, `64`| Default card size in MBit          |
| FlippedScreen | `ON`, `OFF`               | Flip the screen horizontally       |

*Note: Make sure there is an empty line at the end of the ini file.*

## Per-Card Configs

Some configuration values can be modified on a per-card basis within a config file named `CardX.ini` in a card folder, where `X` is the card index (e.g., 1, 2, etc.).

- **ChannelName**: Assigns custom names to each channel (slot) on the card.
- **MaxChannels**: Sets the maximum number of channels for this card.
- **CardSize**: Sets the card size in MBit for this card.

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
MaxChannels=8  # Maximum number of channels for this card
CardSize=4     # Card size in MBit for this card
```

## Splash Screen

By default, FlipperMCE comes with a special splash screen resembling the project's logo.

If you want to customize your splash screen, go to [SplashGen](splashgen/splashgen.html).

From there, you can customize a splash screen to your needs. Once you are happy with the result displayed in the preview, press the **Download UF2** button. This will generate a UF2 file containing your splash screen.

You can flash this splash screen just like any other firmware update.

The flashed splash screen is maintained after a firmware update, so you probably only need to upload it once.

*Note: When combining the splash screen with a firmware UF2 (such as for mass production or flashing multiple FlipperMCEs with the same splash and firmware combination), it's strongly recommended to flash the combined image with `picotool`, since uploading using the usual firmware update procedure often does not work. To do so, please install `picotool` and run:*

```sh
picotool load <combined_file_name>.uf2
```

*while having the FlipperMCE to be updated connected in bootloader mode.*
