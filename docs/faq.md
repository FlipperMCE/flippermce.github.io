
# Frequently Asked Questions (FAQ)


## Is FlipperMCE a clone of 8BitMods MemCard Pro?

It is not! 8BitMods uses completely different hardware and software. Moreover, they have features implemented that will never make their way to *FlipperMCE*.

|             | FlipperMCE    | MemCard Pro GC       |
|-------------|---------------|----------------------|
| MCU         | RP2040        | ESP32                |
| Open Source | ✓             | ✗                    |
| GameCube Support | ✓        | ✓                    |
| Wii Support | ✓             | ✓                    |
| Card Sizes  | 59 - 1019     | 59 - 1019            |
| Wi-Fi       | ✗             | ✓                    |
| Game ID     | ✓             | ✓                    |
| GameID Mapping | ✓          | ✗                    |

While FlipperMCE has its own completely independent code base, we are still very grateful for many useful hints from the *8BitMods* team about certain issues we found during development.


## Will FlipperMCE add a Web Interface?

Since the current hardware is really at its timing limit, there is no room for adding a web interface.


## My Wii will not recognize the card as a memory card

Within the Wii System Menu, the card may occasionally not be recognized. If this happens, please try the following things:

- Close and re-open the GameCube Card Browser
- Switch the mounted card using the buttons on FlipperMCE
- Re-plug FlipperMCE

## All my cards are displayed as corrupted. What is wrong?

Please check your *Encoding* in your card settings.

Each card is (by default) formatted either in "world" or Japanese region. If the region does not match your GameCube/Wii or your game, it will display as corrupted.

As a rule of thumb:

- NTSC-J BIOS cannot access world cards
- NTSC-U/PAL BIOS cannot access Japanese cards
- Regional games for Japan cannot access world cards
- Regional games for other regions cannot access Japanese cards

If you change the *Encoding* setting, all new cards (except Game ID cards) will be formatted with this encoding.

**WARNING:** Existing cards will keep their encoding until they are formatted through the GameCube/Wii. Formatting will result in data loss of this card!

## Can I load game from my FlipperMCE?

As of now, this is not possible.

## Can I connect my FlipperMCE to USB to browse my files?

No. Please use an SD Card reader to read your card images.