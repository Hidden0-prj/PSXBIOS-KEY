# PSXBIOS-KEY

## What it does

PSXBIOS-KEY patches the original Sony 4.1 BIOS disc authentication and boot sequence to unlock CD-R boot, and adds disc-based Game ID, cheats, in-game reset, UniROM, and an MMCE SD app launcher.

[Download the Windows patcher, cheats database, and app launcher](https://github.com/Hidden0-prj/PSXBIOS-KEY/releases/tag/v0.44)

## Features and controls

Hold a shortcut while turning on the console.

- **Select · BIOS Config.** Change the default boot option, choose the cheats source, or turn in-game reset on or off. Use **Save Settings** to keep your changes on the flash chip.
- **Start · Cheats Manager.** Use **Detect Game** to open cheats for the inserted disc, or **Game List** to browse. The in-game cheats menu is off by default and can be enabled in Config.
- **L1 · UniROM.** Opens UniROM 8.0.K.
- **R1 · Fast Boot.** Starts the disc through the faster boot path.
- **R2 · Quick Launch Apps.** Opens the app list on a compatible MMCE SD card. Press **Triangle** to refresh the list.
- **In-game reset.** With IGR enabled, press **L2 + R2 + Select + X** to reboot the console. This BIOS IGR hook supports games launched through its own boot path. Games launched through UniROM do not use it.

Disc-based Game ID lets compatible memory cards select a save card for the game you boot. In the Sony Memory Card Manager, **L2/R2** switch MMCE cards and **L1/R1** switch channels.

### Screenshots

**BIOS Config**

<img src="images/bios-config.png" alt="BIOS Config" width="380" height="285">

**Cheats Manager**

<img src="images/cheats-manager.png" alt="Cheats Manager" width="380" height="285">

**SD2PSX Games List**

<img src="images/game-list.png" alt="SD2PSX Games List" width="380" height="285">

**Select Cheats**

<img src="images/loaded-cheats.png" alt="Select Cheats" width="380" height="285">

**R2 Quick Launch Apps**

<img src="images/r2-apps.png" alt="R2 Quick Launch Apps" width="380" height="285">

**Fast Boot**

<img src="images/fast-boot.png" alt="Fast Boot" width="380" height="285">

**PlayStation BIOS Browser**

<img src="images/psx-bios-browser.png" alt="PlayStation BIOS Browser" width="380" height="285">

**MMCE Detected**

<img src="images/mmce-detected.png" alt="MMCE Detected" width="380" height="285">

**UniROM**

<img src="images/unirom.png" alt="UniROM" width="380" height="285">

**PS1 Full Flasher**

<img src="images/ps1-full-flasher.png" alt="PS1 Full Flasher" width="380" height="285">

**Windows Patcher**

<img src="images/windows-patcher.png" alt="Windows Patcher" width="720">

## Setup

### Flash adapter

This release targets a **512 KiB SST39VF040**. Electroanalog's PSX Flash BIOS project has 32-pin and 40-pin adapter designs, installation photos, and programmer examples. Match the adapter to your motherboard. For in-console flashing, the installed adapter must be wired for console-controlled writes. The upstream build that ties write enable high is read-only in the console. [Electroanalog's PSX-Flash-BIOS guide](https://github.com/Electroanalog/PSX-Flash-BIOS)

[![Electroanalog's 40-pin and 32-pin PSX Flash BIOS adapters](https://raw.githubusercontent.com/Electroanalog/PSX-Flash-BIOS/main/img/psx_fb40-32.png)](https://github.com/Electroanalog/PSX-Flash-BIOS)

Config saving and in-console flashing require a writable **WE#** connection. On the tested **SCPH-7501 / PU-22**, connect flash WE# to **CPU pin 100, /WR0**. Remove any direct WE-to-VCC bridge first. A **10 kΩ pull-up to 3.3 V** can remain. Verify the CPU pinout for your motherboard. [CPU pinout](https://psx-spx.consoledev.net/pinouts/#pinouts-cpu-pinouts)

### Patch your BIOS in Windows

Use your own original Sony 4.1 BIOS dump. Each supported file is **524,288 bytes**. The filenames below are for identification. The patcher checks the actual file and rejects other dumps.

- **USA / NTSC-U/C** · SCPH-7001 / SCPH-7501 family · CRC32 **502224B6**  
  `Sony PlayStation SCPH-7001 BIOS v4.1 (1997-12-16)(Sony)(US).bin`
- **Europe / PAL** · SCPH-7502 family · CRC32 **318178BF**  
  `Sony PlayStation SCPH-7502 BIOS v4.1 (1997-12-16)(Sony)(EU).bin`

Open **PSXBIOS-KEY-Patcher.exe**, choose your BIOS file and an output folder, then click **Apply Patch**.

The patcher creates a **BIOS BIN** for a chip programmer, a **self-contained PS1 flasher** (`.psexe`) with the BIOS already inside, and a **BIN/CUE flasher disc** with 50 MiB of padding.

### Install on a PlayStation

- **Fresh installation.** Program the generated BIOS BIN onto the SST39VF040 with your external programmer, verify it, then install the chip and adapter.
- **Adapter already installed.** With a working console and writable WE# wiring, load the generated self-contained PS1 flasher through UniROM/NOPS, or burn the generated CUE and boot the flasher disc. Keep its matching BIN beside the CUE when burning. In R2 Apps, give the flasher an `.exe` extension and put it in `Apps/`.
- **Flash.** Check the region and chip ID **BF D7**, press **X**, and wait until all 524,288 bytes are verified. Press **Start + Select** to reboot.

Full Flash writes the entire chip and resets BIOS settings. Keep power on until verification finishes. If the console can no longer boot after a failed write, use an external programmer to restore your backup. Version 0.44 is a test release. Physical console verification is pending.

### Set up the MMCE : Memcardpro/sd2psx SD card

For now, the SD features require the latest compatible **sd2psXtd firmware with PS1 MFS1 filesystem support**. Check your device against the [firmware releases and installation guide](https://github.com/sd2psXtd/firmware/releases).

1. Download and extract **PSXBIOS-KEY-0.44.zip** from the [release page](https://github.com/Hidden0-prj/PSXBIOS-KEY/releases/tag/v0.44).
2. Copy **Apps** from **MMCE SD Setup / Copy to SD card of MMCE** to your SD card root. Keep **BOOT.EXE**. Open **Cheats / US**, **EU**, or **JP**, and copy that region's **Cheats** folder to the SD card root. Choose one region because each has its own Game List index.
3. Hold **Select** at boot, set **Cheats** to **SD2PSX**, and save. Hold **Start** at boot for **Detect Game** or **Game List**. Select the codes you want before starting the game.
4. Put your PS1 `.exe` apps in **Apps** and hold **R2** at boot. Press **Triangle** to refresh after adding files. RAM Tester, no$cash, and 240p are examples of apps you can add yourself.

The folders include short READ ME notes. Cheat selections last for the current boot. JP contains Japanese cheats. The patcher accepts the supported USA and PAL BIOS dumps.

## Credits

- **xyz** for [SD2PSX](https://github.com/sd2psx/firmware), the [sd2psXtd Team](https://github.com/sd2psXtd), and [bbsan2k](https://github.com/bbsan2k).
- **jdfr228** for [PS1 Disc-Based Game ID](https://github.com/jdfr228/PS1-Disc-Based-Game-ID).
- **spicyjpeg** and contributors for [ps1-bare-metal](https://github.com/spicyjpeg/ps1-bare-metal).
- **Sickle**, **JonathanDotCel**, and the contributors to [UniROM](https://github.com/JonathanDotCel/unirom8_bootdisc_and_firmware_for_ps1).
- **Electroanalog** for the [PSX Flash BIOS adapters and photos](https://github.com/Electroanalog/PSX-Flash-BIOS).

