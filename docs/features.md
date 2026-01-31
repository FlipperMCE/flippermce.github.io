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
DL-DOL-GT4P-EUR=FolderName
```

In this case, *FolderName* refers to a folder located under `/MemoryCards/GC`.

*Note: Make sure there is an empty line at the end of the ini file.*

If you want to use a preconfigured mapping containing all known Cross-Save Titles, feel free to download [this file](assets/Game2Folder.ini) by *R3Z3N*.

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

### Card splashes (1.1.0)

Add a splash image that the device shows in the card browser. Use the [SplashGen](splashgen/splashgen.html) to convert a source image to the device `.bin` format, then place the generated file in the card folder on your SD card.

Naming and behavior
- Folder-level splash (default for the folder):
    - Path: `MemoryCards/GC/<card_folder>/<card_folder>.bin`
    - Example: `MemoryCards/GC/SuperGame/SuperGame.bin` — used when no channel-specific image exists.
- Channel-specific splash (overrides folder-level for that channel):
    - Path: `MemoryCards/GC/<card_folder>/<card_folder>-<channel_number>.bin`
    - Example: `MemoryCards/GC/SuperGame/SuperGame-1.bin` — shown only for channel 1 of that card folder.
- Fallback rules:
    - If a channel-specific file exists it is used.
    - Otherwise the folder-level `<card_folder>.bin` is used.
    - If neither exists, no splash is shown.

Practical notes
- `<channel_number>` matches the on-device channel index (1..N).
- Filenames must match exactly; FAT SD cards are usually case-insensitive but keep names consistent.
- Use `misc/splashgen.html` to produce correctly-sized and packed `.bin` files for the OLED.
- Keep names short — very long filenames may cause display or performance issues.
- Store splash `.bin` files alongside that card's `CardX.ini` and save data in the same folder.

### Block Device Interface (1.1.0)

FlipperMCE can be accessed as a block device through GameCube and Wii applications. This feature allows direct read/write access to the sd card storage at a block level. To use this functionality, applications must implement the MMCE (Multipurpose Memory Card Emulator) protocol, which is documented in detail in the [memcardpro.txt](https://github.com/FlipperMCE/firmware/blob/143044d067805e424b9267949c0c64b18f61ec91/doc/mcp/memcardpro.txt) specification.

**Development Support:**
- The latest version of libOGC2 includes built-in support for this protocol
- Suitable for custom tools and applications that need direct memory card access
- Enables advanced features like backup/restore utilities or save managers

#### Compatible Apps

Thanks to many other developers like extrems, there are already plenty of homebrew apps that support FlipperMCE as a Block Device:

- [240p Test Suite](https://artemiourbina.itch.io/240p-test-suite) (pending release)
- [Blockamok Remix](https://mode8fx.itch.io/blockamok-remix) (pending pull request)
- [ClassiCube](https://www.classicube.net/download/gamecube)
- [CleanRip](https://github.com/emukidid/cleanrip)
- [CubeSX](https://github.com/emukidid/pcsxgc) (pending release)
- [Enhanced mGBA](https://github.com/extremscorner/emgba)
- [FCE Ultra GX](https://github.com/dborth/fceugx) (pending release)
- [Game Boy Interface](https://www.gc-forever.com/wiki/index.php?title=Game_Boy_Interface)
- [GC HTTP Server](https://github.com/emukidid/gchttpserver)
- [GCC Test Suite](https://github.com/greenwave-1/GTS)
- [Not64](https://github.com/extremscorner/not64)
- [Octave](https://github.com/mholtkamp/octave) (pending release)
- [Scratch Everywhere!](https://github.com/ScratchEverywhere/ScratchEverywhere)
- [Snes9x GX](https://github.com/dborth/snes9xgx) (pending release)
- [SuDokuL](https://mode8fx.itch.io/sudokul) (pending pull request)
- [Swiss](https://github.com/emukidid/swiss-gc) (Config File and File Management)
- [Trogdor: Reburninated](https://mode8fx.itch.io/trogdor-reburninated) (pending pull request)
- [Visual Boy Advance GX](https://github.com/dborth/vbagx) (pending release)
- [WakeMii](https://github.com/emukidid/wakemii)