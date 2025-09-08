<p align="center">
    <img src="images/FlipperMCE.svg" alt="FlipperMCE Logo" width="20%">
</p>

# FlipperMCE Firmware

I'm excited to present you a project I've been working on the last 6 months: **FlipperMCE**.

**FlipperMCE** is a fully Open Source Nintendo GameCube Memory Card Emulator (MCE), based on the famous **sd2psx** Playstation 2 MCE designed by @xyzz.

It implements the GameCube Memory Card protocol and therefore is able to emulate cards from 59 Blocks (0.5 MB / 4 MBit) up to 1019 Blocks (8 MB / 64 MBit).

Every Card image is saved as a dedicated *.raw* file in the respective folder on SD card.


## 🚀 Features

- Emulation of Cards from 59 Blocks - 1019 Blocks
- GameID supplied by swiss or any other Game Loader that supports it (CubeBoot, Nintendont, ...)
- BootCard support (boot to cards in BOOT/ folder if activated)
- Multi Region support (creates new cards either in JPN or World encoding)

For more info, see [Features](features.md)


## ❤️ Special Thanks to...

- **Vapor, rippenbiest, Mancloud, @hitmanmcc**: for beta testing ❤️
- **@gameBitfunx**: for PCB design, testing and support ❤️
- **@xyz**: for sd2psx ❤️
- **sd2psXtd Team**: (you know who you are 😉 )
- **8BitMods Team**: for helping out with card formatting and providing lots of other useful information for things like unlock ❤️
- **@extrems**: For insights into EXI communications and libOGC2 SDK

