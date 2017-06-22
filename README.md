# mpd_kb_control
Control bash-script for mpd that uses mpc
# Requirements
 * `mpd` and `mpc`
 * a keyboard with multimedia keys
# Installation
```
git clone https://github.com/nogaems/mpd_kb_control.git
cp mpd_kb_control/mpd_kb_control /path/to/your/local/binaries/
```
If you have not the path that intended for local binaries, either you have to create it by yourself and add to your $PATH environment variable:
```
mkdir ~/.local/bin -p
echo 'PATH=$PATH:~/.local/bin' >> ~/.bashrc
```
or just use your global binaries path `/usr/bin/` (actually it's the worse way). This case you have to be root.
# Configuration

I do use `dwm`, so I added some bindings to my configuration header file, like this:
```
...
/* MPD keyboard controls sections */
static const char *mpd_play []  = { "mpd_kb_control", "play", NULL };
static const char *mpd_next []  = { "mpd_kb_control", "next", NULL };
static const char *mpd_prev []  = { "mpd_kb_control", "prev", NULL };
static const char *mpd_raise [] = { "mpd_kb_control", "raise", NULL };
static const char *mpd_lower [] = { "mpd_kb_control", "lower", NULL };
static const char *mpd_mute []  = { "mpd_kb_control", "mute", NULL };

static Key keys[] = {

...

        { NULL,                         XF86XK_AudioPlay, spawn,   {.v = mpd_play } },
        { NULL,                         XF86XK_AudioNext, spawn,   {.v = mpd_next } },
        { NULL,                         XF86XK_AudioPrev, spawn,   {.v = mpd_prev } },
        { NULL,                         XF86XK_AudioRaiseVolume, spawn,   {.v = mpd_raise } },
        { NULL,                         XF86XK_AudioLowerVolume, spawn,   {.v = mpd_lower } },
        { NULL,                         XF86XK_AudioMute, spawn,   {.v = mpd_mute } }
...
```
then rebuild `dwm` through `emerge`. That's it.
# Usage
 * The first pressing on `XF86XK_AudioPlay` will start playing music if it was paused or stoppped (if stopped, the first track in playlist will be played), otherwise music will be paused.
 * Usage of Next/Prev and RaiseVolume/LowerVolume buttons is obvious.
 * `XF86XK_AudioMute`: If the current volume value is not 0, it will be setted to 0. If it's currently 0, the previous value that was established manually will be restored.
