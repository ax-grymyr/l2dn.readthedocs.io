# Client

The server works with any Classic client with 447 protocol. You can [download](#download-the-patched-client) the ready-to-run client or [patch](#steps-to-patch-the-official-client) the official client manually.


## Download the patched client

Patched EU client for 447 protocol: [link](https://drive.google.com/file/d/1Sv7yYdxNFtj4U-_Zo9TvD5WTrE3wFNh4/view?usp=sharing).

RU patch (from RU classic client): [link](https://drive.google.com/file/d/1LrfIicy1oZLVVl6AJyu_8NCkMvZ47L1P/view?usp=sharing).

Use [7-zip](https://7-zip.org/) to extract the client from the archive and run `L2.exe`. The client is configured to connect to `localhost`, port `2106`.


## Steps to patch the official client

### 1. Download the official client

You can download client from [http://akumu.ru](http://akumu.ru) website. Any client for 447 protocol should work.

I use [`L2EU-P447-D20240327-P-230809-240401-1`](http://akumu.ru/lineage2/L2EU/P447/L2EU-P447-D20240327-P-230809-240401-1/) client version for testing the server.

### 2. Patching the client

- Download [`patcher.7z`](https://drive.google.com/file/d/1cL0Zl2dPKFIDr60VNS759TNmYRVaL4Y7/view?usp=sharing) and [`dsetup.dll.7z`](https://drive.google.com/file/d/1Tg48f7gmkAp1pnUN7EDbnZM81353wW_A/view?usp=sharing).
- Extract `dsetup.dll.7z` to the client's `system` directory, replacing the existing dll.
- Extract `patcher.7z` to the client's `system` directory and run `patcher.exe` from the directory.
- Extract `patcher.7z` to the client's `system\eu` directory and run `patcher.exe` in the directory. It will take some time to patch all `.dat` files.

### 3. `L2.ini` modification

The next step is the modification of `L2.ini`.

- Decrypt `L2.ini` using the command `l2encdec.exe -d L2.ini L2.ini.txt`.
- Open `L2.ini.txt` in any text editor.
- Find and change the following parameters:
  - `ServerAddr=127.0.0.1`
  - `ExternalLogin=false`
  - `CmdLineLogin=false`
  - `FrostModule=false`
  - `UseAutoSoulShotClassic=true`
- Replace `L2.ini` with the modified version using the command `l2encdec.exe -e 413 L2.ini.txt L2.ini`.

Now you can run the server locally and connect with this client to the server.

### 4. Replacing Russian item names with English names (optional)

EU client contains Russian item names for Classic edition for some reason (probably left from Russian Classic client).
To replace Russian item names with English names, replace 2 files from the [item_names.7z](https://drive.google.com/file/d/1F1YlOGZAnfsB3lnhUxEH0eePVspGKOW5/view?usp=sharing).
Put `ItemName_Classic-eu.dat` and `L2GameDataName.dat` files from the archive to the `system\eu` directory of the client.
I generated these 2 files for the `L2EU-P447-D20240327-P-230809-240401-1` client version and they may not work for another version.

!!! note

    The code which replaces Russian item names with English names 
    is currently in `L2Dn/Tools/L2Dn.UnitTests/DatReaderTests.cs`, `ReplaceRuItemNamesInEuClient` unit test.
