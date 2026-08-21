---
description: Instructions on how to get debug logs after an application error.
icon: bug
---

# Debugging

AirPig has two debug capabilties for production builds.

If AirPig fully crashes, it should send a small snippit of data to our servers describing where the crash happened in AirPig source code so we can diagnose and fix it.

But sometimes the engine can have errors that aren't a crash, or a crash can happen while not connected to the internet. In either case, we won't have any information to diagnose and fix a problem. So, AirPig has a logging mode that can be enabled to reproduce a problem and send us the information we need to fix it.

### Enable Logging

Logging to disk is disabled by default because logging has a performance cost that isn't necessary most of the time. To turn on logging, you must launch AirPig with the `-log=text` argument.

#### Logging With Steam

Most users will be using AirPig on Steam. To turn logging on within Steam, you can add the required launch argument by following these instructions:

1. Find AirPig in your Steam library
2. Highlight the game and press the **`...` (three dot) button** on SteamDeck, or click the **Gear Button** on Windows and select **Properties**
3. Under **General**, find the **Launch Options** field
4. Enter exactly: `-log=text`  in the **Launch Options** field
5. Close the **Properties** window and launch the game normally

#### Logging Without Steam

If you are running a build of AirPig outside of steam, you may need to manually launch AirPig with the logging arguments by following these instructions:

1. Open the directory where AirPig is installed using the File Explorer
2. Right click in the directory and choose **Open in Terminal**
3. Type `Airpig.Raylib.exe -log=text`  to launch the engine with logging enabled

### Finding Logs

The engine writes one log file per game launch to the following path on Windows. You can paste this location into the File Explorer's address bar to open this directory:

```
%AppData%/airpig/logs/
```

There will be a list of plain text files for your recent game sessions. The easiest way to provide these log files is to [join our Discord server](https://discord.gg/7knctqb8bX) and ask for help. Avoid sharing log files publicaly.

#### Logs On Steam Deck

Finding the log files on SteamDeck is a bit more tricky as it creates an emulated Windows file system for each installed Game. To find log files on SteamDeck, first switch to **Desktop Mode** and open the file manager. The path for the logs on SteamDeck should be:

```
~/.local/share/Steam/steamapps/compatdata/4994310/pfx/drive_c/users/steamuser/AppData/Roaming/airpig/logs/
```

### What's In The Logs

Log files are plain text so open them up and see! They contain information about what the engine is doing at each step of its process. Sometimes log files contain information about your computer's filesystem - such as the path on disk where your game project is stored. So it's a good idea not to share these publicly on the internet. But the log files are primarily focused on what the engine code is doing during operation and are safe to provide to our team for diagnostics.

### Other Log Options

The `log` launch argument supports three different values:

* `-log=none`  - this is the default, logging is fully off and has no performance impact on the game. This is the log mode used when no launch argument is passed.
* `-log=text`  - this logs to one file per session and is the most commonly-used way to get log information if there is an error or problem.
* `-log=console`  - this logs to the console or STDOUT. This mode is for more advanced users or special builds that may want to look at game-specific logging within Proton or other emulation system's broader logging
