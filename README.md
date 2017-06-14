# fix_display
Simple python script for running arbitrary scripts for different monitor configurations

# Why did I make this?
Because my laptop is picky about exactly how you activate multiple monitors: No other apps/scripts were able to simply enable monitors 1, 2 and 3 on their own. I eventually figured out a work-around hokey-pokey dance that succeeded, but still wanted some kind of "just make it work" automation.

# What does it do?
The script compares the set of connected monitors against a list of configurations: If one matches exactly (not a subset!) then it executes the supplied shell commands. Optionally, you can specify a "transition output" which I found useful for multiple arrangements: The script will invoke xrandr selecting only the transition output and leaving all others off, then it will continue with the desired script.

# Example config file
The script expects to find the config file at: $XDG_CONFIG_DIR/fix_display.json

```json
{
    "configurations": {
        "docked_closed": {
            "outputs": ["DP-0", "DP-1"],
            "command": "xrandr --output eDP-1-1 --off --output DP-0 --auto --output DP-1 --auto --right-of DP-0; feh --bg-tile ~/Documents/Backgrounds/kenblock_nz_5280x1080.png"
        },
        "docked_open": {
            "outputs": ["DP-0", "DP-1", "eDP-1-1"],
            "transition_output": "eDP-1-1",
            "command": "xrandr --output DP-0 --primary --auto --pos 1440x0 --output DP-1 --auto --pos 3360x0; xrandr --output eDP-1-1 --mode 1440x900; feh --bg-tile ~/Documents/Backgrounds/kenblock_nz_5280x1080.png"
        },
        "mobile": {
            "outputs": ["eDP-1-1"],
            "transition_output": "eDP-1-1",
            "command": "xrandr --output eDP-1-1 --primary --mode 1920x1080; feh --bg-tile ~/Documents/Backgrounds/kenblock_nz_1920x1080.png"
        }
    }
}
```
