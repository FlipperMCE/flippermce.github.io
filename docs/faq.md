# FAQs

## Is FlipperMCE a clone of 8BitMods MemCard Pro?

It is not! 8BitMods uses a completely different Hardware, Software.
Moreover, they have features implemented, that will never make their way to *FlipperMCE*.

|             | FlipperMCE    | MemCard Pro GC       |
|-------------|---------------|----------------------|
| MCU         | RP2040        | ESP32                |
| Open Source | X             | /                    |
| GC Support  | X             | X                    |
| wii Support | X             | X                    |
| Card Sizes  | 59 - 1019     | 59 - 1019            |
| Wi-Fi       | /             | X                    |
| Game ID     | X             | X                    |
| GameID Mapping | X          | /                    |

While FlipperMCE has its completely own code base, we are still very grateful for many useful hints from *8BitMods* team about certain issue we found during development.


## Will FlipperMCE add a Web Interface ?

Since the current hardware is really at its limit timing wise, there is no room for adding a Web Interface.


##  My wii will not recognize the card as memory card

Within the wii System Menu, the card may occasionally not be recognized. If this happens please try the following things:

- Close and re-open Gamecube Cardbrowser
- Switch the mounted card using the buttons on FlipperMCE
- Re-Plug FlipperMCE

## All my cards are displayed as corrupted. What is wrong?

Please check your *Encoding* in your card settings.

Each card is (by default) formatted either in world or japanese region. If the region does not match your gamecube/wii or your game, it will display as corrupted.

As a rule of thumb:

- NTSC-J BIOS cannot access world cards
- NTSC-U/PAL BIOS cannot access japanese cards
- Regional games for Japan cannot access world cards
- Regional games for other regions cannot access japanese cards

If changing the *Encoding* Setting, all new cards that are not Game ID cards are formatted with this encoding.

**WARNING: Existing Cards will keep their encoding until they are formatted through the GameCube/wii. Formatting will result in data loss of this card!**

