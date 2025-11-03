# Proton Launch Options

My personal resource compiling and documenting useful Launch Options for Proton on Steam.

## Tools

### GameMode

> allows games to request a set of optimisations be temporarily applied to the host OS and/or a game process

- `gamemoderun %command%`

More information on [ArchWiki](https://wiki.archlinux.org/title/GameMode).

### MangoHud

> overlay for monitoring system performance while inside applications and to record metrics for benchmarking

- `mangohud %command%`
- `mangohud gamemoderun %command%`

Default Keybinds:

- `RShift+F12` – Toggle overlay
- `RShift+F11` – Change overlay position
- `RShift+F10` – Toggle preset
- `LShift+F2`  – Toggle logging
- `LShift+F4`  – Reload config

Obs.: `RShift+F11` normally coincides with Steam Overlay's toggle keybind.

You can set options with `MANGOHUD_CONFIG=`. A config I used was `MANGOHUD_CONFIG=vsync=2,fps_limit=240`.
You can use GOverlay* or Mangojuice (recommended) to more easily edit MangoHud's config files.

More information on [ArchWiki](https://wiki.archlinux.org/title/MangoHud).

*I have yet to try GOverlay. Sorry.

### DXVK_HUD

DXVK's native, zero-overhead overlay (bundled by Proton). Minimalist alternative to MangoHud for monitoring performance and benchmarking.

- `DXVK_HUD=1 %command%`
- `DXVK_HUD=full %command%`

> Additionally, `DXVK_HUD=1` has the same effect as `DXVK_HUD=devinfo,fps`, and `DXVK_HUD=full` enables all available HUD elements.

Aditional info on [DXVK's README section on HUD](https://github.com/doitsujin/dxvk/blob/master/README.md#hud).

## Games

### Hollow Knight: Silksong (Native Linux)

Oops! These are not Launch Options for Proton, but rather for the native version of the game!

The game runs great on Linux, constant 240 fps with vsync on on my machine. But a compatibility problem with _Wayland_ made the video cutscenes run at half-speed, while their sound ran at normal speed, ruining the experience and even potentially spoiling what hadn't been shown on screen next.
Fortunately, it seems that `STEAM_COMPAT_RUNTIME_SDL2=1` and `--force-vulkan` (not sure which, _and_ or _or_), manages to fix the issue.

In _Game Properties_, _Compatibility_, check _"Force the use of a specific Steam Play compatibility tool"_ and select _"Steam Linux Runtime 1.0 (scout)"_. Then set your Launch Options in _General_.

- `STEAM_COMPAT_RUNTIME_SDL2=1 MANGOHUD_CONFIG=vsync=2,fps_limit=240 mangohud gamemoderun %command% --force-vulkan`

### Shapez 2 (Native Linux)

Oops! These also are for the native version of the game, who also appeared to have some problems with _Wayland_.
I'm running this also with _"Steam Linux Runtime 1.0 (scout)"_.

- `SDL_VIDEODRIVER=wayland gamescope -w 1920 -h 1080 -r 60 --mangoapp -f -- gamemoderun %command%`

### Misc

Found this online and I'm not sure about the specifics. I'm yet to research these options and _vkBasalt_.

- `VKD3D_FEATURE_LEVEL=12_1 PULSE_LATENCY_MSEC=60 DXVK_ASYNC=1 WINE_FULLSCREEN_FSR=1 ENABLE_VKBASALT=1 gamemoderun %command%`
