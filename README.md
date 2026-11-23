# PSXBIOS-KEY

PSXBIOS-KEY is a custom BIOS for the original PlayStation. It keeps the Sony startup animation and sound and adds disc boot shortcuts, disc-based Game ID, cheats, in-game reset, and an app launcher for MMCE cards.

**This release is for 512 KiB SST39VF040 flash installations.** You'll need an exact original Sony 4.1 BIOS dump and a compatible console, adapter, and programmer for first installation. BIOS 0.44 is a test release for USA and PAL. Start with a spare chip and keep a verified backup of your current BIOS.

[Download the 0.44 test release](https://github.com/Hidden0-prj/PSXBIOS-KEY/releases/tag/v0.44)

## What it does

- Keeps the Sony shell, memory card manager, startup visuals and sound.
- Adds native CD-R boot and a Fast Boot shortcut. Drive condition and disc quality still matter.
- Sends the game's ID when booting a disc so compatible hardware can select its save card or profile. This builds on [jdfr228's PS1 Disc-Based Game ID](https://github.com/jdfr228/PS1-Disc-Based-Game-ID).
- Includes UniROM 8.0.K with an L1 boot shortcut.
- Adds a Cheats Manager with game detection and sources for a compatible SD2PSX cheats database or standard memory card. The in-game cheats menu is off by default.
- Adds optional in-game reset and flash-backed BIOS settings.
- Adds MMCE card and channel switching in the Sony memory card manager. With a compatible device, use L2/R2 for cards and L1/R1 for channels.
- Can launch PS1 executables from the `Apps` folder of an MFS1-capable MMCE device. Quick Launch Apps 1.4 shows the installed BIOS version and region and gives more detailed SD errors.

## Which BIOS dump do I need?

Use a clean, unmodified dump of the original BIOS from your console. The following names are useful for identifying your own dump. Each file must be exactly **524,288 bytes**.

- **USA / NTSC-U/C, Sony 4.1, SCPH-7001/7501 family**  
  `Sony PlayStation SCPH-7001 BIOS v4.1 (1997-12-16)(Sony)(US).bin`  
  Original CRC32 **502224B6** · MD5 `1e68c231d0896b7eadcad1d7d8e76129`  
  Original SHA-256 `39dcc1a0717036c9b6ac52fefd1ee7a57d3808e8cfbc755879fa685a0a738278`  
  Patched 0.44 CRC32 **E06FCC1B**
- **Europe / PAL, Sony 4.1, SCPH-7502 family**  
  `Sony PlayStation SCPH-7502 BIOS v4.1 (1997-12-16)(Sony)(EU).bin`  
  Original CRC32 **318178BF** · MD5 `b9d9a0286c33dc6b7237bb13cd46fdee`  
  Original SHA-256 `5e84a94818cf5282f4217591fefd88be36b9b174b3cc7cb0bcd75199beb450f1`  
  Patched 0.44 CRC32 **D37B13E5**

The patcher identifies the dump by its contents. The name is only a reference. Japan and other BIOS revisions are outside this release.

## Patch your BIOS on Windows

1. Download and open **PSXBIOS-KEY-Patcher.exe**. The title bar should say **BIOS 0.44**.
2. Browse to your original BIOS BIN. The patcher displays the region and verified CRC32, and checks the full SHA-256 before patching.
3. Pick an output folder and click **Apply Patch**.

The patcher includes its tools and the UniROM component. It creates a full BIOS BIN, a self-contained PS1 **Full Flash 1.0** executable (`.psexe`), and a flasher disc (`.bin` and `.cue`). The disc includes 50 MiB of padding. A rejected input creates no output.

## Put it on a console

- **Blank or loose flash chip** · Program the generated BIOS BIN on an external programmer, such as a T48 with the right adapter. Verify the readback. A console needs a working BIOS before it can run the PS1 flasher.
- **Running console** · If you already have a writable SST39VF040 and a working PS1 executable loader, launch the generated flasher through UniROM/NOPS. To list the flasher in R2 Apps, give the PS-X executable an `.exe` extension before placing it in `Apps`. Check the region, CRC32 and chip ID **BF D7** before pressing **X**.
- **Flasher disc** · Burn the `.cue` as a disc image and keep its companion BIN beside it. This route requires a console that can boot the CD-R. Burned-disc behavior for this release still needs hardware testing.

The full flasher replaces all 512 KiB, including BIOS settings. Keep the console powered on through verification. The old built-in serial flasher was removed in 0.44. Keep an external programmer available for recovery. Future protected updates require the matching boot core, and the 0.43 protected updater cannot install 0.44.

## Boot shortcuts

Hold the button while powering on.

- **Select** opens BIOS configuration.
- **Start** opens the Cheats Manager.
- **L1** opens UniROM.
- **R1** opens Fast Boot.
- **R2** opens Quick Launch Apps from a compatible MMCE SD card.

With in-game reset enabled, press **L2 + R2 + Select + X** to reboot during a supported game.

## Set up R2 Apps

Extract **SD-Apps-Launcher-1.4.zip** to the root of the MMCE SD card so it has `Apps/BOOT.EXE`. Put your own PS1 `.exe` files in the same folder. Hold R2 at boot and use Triangle to refresh the list after adding files. This requires PS1 MFS1 filesystem support on the card. The launcher download is separate from card firmware and the optional cheats database.

## Credits

- **jdfr228** for the original [PS1 Disc-Based Game ID](https://github.com/jdfr228/PS1-Disc-Based-Game-ID) work.
- **spicyjpeg** and contributors for [ps1-bare-metal](https://github.com/spicyjpeg/ps1-bare-metal).
- **Sickle**, **JonathanDotCel**, and the UniROM contributors for [UniROM and the PS1 homebrew tools](https://github.com/JonathanDotCel/unirom8_bootdisc_and_firmware_for_ps1).
- The [ps1-mmce contributors](https://github.com/sd2psXtd/firmware) and the authors of [MKPSXISO](https://github.com/Lameguy64/mkpsxiso), [xdelta](https://github.com/jmacd/xdelta), and [7-Zip](https://www.7-zip.org/) for their tools.
