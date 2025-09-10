<p align="center">
    <img src="images/FlipperMCE.svg" alt="FlipperMCE Logo" width="20%">
</p>


# FlipperMCE Firmware

I'm excited to present a project I've been working on for the last 6 months: **FlipperMCE**.


**FlipperMCE** is a fully open source Nintendo GameCube Memory Card Emulator (MCE), based on the famous **sd2psx** PlayStation 2 MCE designed by @xyzz.

It implements the GameCube Memory Card protocol and is able to emulate cards from 59 blocks (0.5 MB / 4 MBit) up to 1019 blocks (8 MB / 64 MBit).

Each card image is saved as a dedicated *.raw* file in its respective folder on the SD card.



## Features

- Emulation of cards from 59 to 1019 blocks
- GameID supplied by Swiss or any other game loader that supports it (CubeBoot, Nintendont, etc.)
- Multi-region support (creates new cards in either JPN or World encoding)

For more info, see [Features](features.md).



## Special Thanks

- **Vapor, rippenbiest, Mancloud, @hitmanmcc**: for beta testing ❤️
- **@gameBitfunx**: for PCB design, testing and support ❤️
- **@xyzz**: for sd2psx ❤️
- **sd2psXtd Team**: (you know who you are 😉)
- **8BitMods Team**: for helping out with card formatting and providing lots of other useful information for things like unlock ❤️
- **@extrems**: for insights into EXI communications and libOGC2 SDK

