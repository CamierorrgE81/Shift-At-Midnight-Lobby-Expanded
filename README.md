# Midnight Lobby Expanded

A BepInEx 6 IL2CPP mod for increasing the player capacity of newly created Photon Fusion rooms in Shift At Midnight.

## Installation

1. Close Shift At Midnight and Steam.
2. Download `MidnightLobbyExpanded-0.1.0.zip` from the GitHub release.
3. Extract the contents of the archive into the game installation directory, the directory containing `ShiftAtMidnight.exe`.
4. Start the game through Steam. The first launch generates BepInEx interop assemblies and can take longer than usual.
5. Confirm that `BepInEx/LogOutput.log` contains both of these lines:

```text
Loading [Midnight Lobby Expanded 0.1.0]
Patched Fusion.NetworkRunner.StartGame. New rooms will allow 10 players.
```

6. Every player joining the lobby must install the same release version.

The release package contains BepInEx 6 IL2CPP, its required .NET runtime, and the plugin. It does not contain game files, saves, configuration files, logs, or generated interop assemblies.

## Configuration

After the first start, edit:

```text
BepInEx\config\io.github.shiftatmidnight.midnightlobbyexpanded.cfg
```

`Lobby.MaxPlayers` defaults to `10` and accepts values from `1` to `10`. Restart the game after changing it.

## Behavior

The mod patches `Fusion.NetworkRunner.StartGame` and sets `StartGameArgs.PlayerCount` to the configured capacity before a room is created.

Every person joining the same room needs the same mod version. This patch changes Fusion's room capacity only. The game may also have player-slot, spawn-point, UI, and gameplay assumptions that need separate patches before a 10-player match is fully playable.

## Uninstall

When this is the only BepInEx installation in the game directory, remove these items from the game directory:

```text
BepInEx
dotnet
.doorstop_version
doorstop_config.ini
winhttp.dll
changelog.txt
```

Keep BepInEx in place when it is shared by other mods; remove only `BepInEx\plugins\MidnightLobbyExpanded` to uninstall this plugin.

## Build From Source

The project expects a BepInEx 6 IL2CPP installation in the parent game directory.

```powershell
dotnet build
```

After a successful build, the plugin is copied to:

```text
..\BepInEx\plugins\MidnightLobbyExpanded\MidnightLobbyExpanded.dll
```

## License

MIT. The repository contains only mod source code and no game assets or game binaries.
