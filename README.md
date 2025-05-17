# menus

2 similar logic Bash scripts to connect to a Wi-Fi network / Bluetooth device with a launcher.

## Features

- Enable/Disable Wi-Fi / Bluetooth device
- Connect/disconnect to Wi-Fi network / Bluetooth device
- Desktop notifications via notify-send
- Translate to your language by modifying script variables in a configuration file
- Can be use with your preferred launcher:
	- wofi
	- rofi
	- wmenu
	- dmenu
	- bemenu
  - walker
	- Or a custom one!

## Network features
  - Select the Wi-Fi interface to use
  - Connection options: forget, DNS, static IP...
  - Wireguard support
  - Connect to a hidden Wi-Fi network
  - Shows if Wi-Fi network is secure via WPA 1/2
  - Shows signal level visually
  - A submenu to contain all of the above options

## Considerations

- Does not show Wi-Fi networks with WEP security
- When using this script with dmenu launcher, the botton to hide passwords does not work

## Dependencies

### Required

- Bash
- A menu launcher
- A [Nerd Fonts](https://www.nerdfonts.com/) font or a font that support emojis

### Optional

- libnotify for notifications
- NetworkManager for wifi and wireguard
- bluetoothctl (provided by bluez-utils in Arch) and bc for bluetooth

## Translation and customization

### Configuration file location

The following files are sourced in the corresponding order. If one of the files is found, the following files will not be searched:

1. \$XDG\_CONFIG\_HOME/\$program\_name/config
2. \$HOME/.config/\$program\_name/config
3. \$HOME/.\$program\_name

The variable `program_name` is set to `basename $0`.

Any modification of the program can be made in the configuration file to avoid losing modifications when updating the script.
Command line options overwrite this file.

### Variables for configuration file

Some variables of interest may be:

- **launcher**: A string defining the launcher (default is 'walker'). The possible values are:
	- wofi
	- rofi
	- wmenu
	- dmenu
	- bemenu
  - walker
	- custom
- **custom_opts**: It's an asosiative array with 4 values that must be set when `launcher` variable is set to 'custom'.
	- **custom_opts[launcher]**: Launcher command or path.
	- **custom_opts[insensitive]**: Launcher options for case-insensitive input.
	- **custom_opts[sensitive]**: Launcer options for case-sensitive input.
	- **custom_opts[password]**: Launcher options for password-prompt mode.
- **submenu**: If set, shows Wi-Fi options in a submenu (unset by default).
- **emoji**: If set, shows emoji icons instead of Nerd Fonts icons.
- **wireguard**: If set, shows wireguard connections option in the main manu (unset by default).
- **notifications**: If set, sends desktop notifications (if notify-send can be found by the user's PATH, then it is set).

That a variable is set means that it has a value assigned to it (any value). For example:

```sh
launcher='walker'    # It's set
submenu=1          # It's set
wireguard=         # It's not set
```

### Custom launcher syntax

The custom launcher options must be given with the corresponding dashes.

```sh
# In config file
custom_opts[launcher]='wofi'
custom_opts[insensitive]='--dmenu --insensitive --prompt'
custom_opts[sensitive]='-d -p'
custom_opts[password]='--dmenu --password -p'

# or

# In command line
--custom wofi '--dmenu --insensitive --prompt' '-d -p' '-d --password --prompt'
```

Note that the last flag must be the one to set the prompt.

If your launcher don't support password prompt, just set it case-sensitive.

### Icons

By default Nerd Fonts icons are use. If you don't want to use a Nerd Fonts font, emojis can be use for icons.

```sh
# In config file
emoji=1

# or

# In command line
--emoji
```

Each icon can be customized in the configuration file setting the icon_* variables:

Which icon does each variable belong to? Find out on your own, to much documentation.

If you customize the icons, it's better to set just one character (UTF-8 is fine) for each one,
as it could have unexpected behavior otherwise, or not, it is just not tested.

### Translation
All the tr_* variables can be changed in the the configuration file to translate the text.

## Wireguard support

The wireguard connection must already exist. To import a wireguard profile FILE.conf:
```sh
sudo nmcli connection import type wireguard file /PATH/TO/FILE.conf
```
Replace `/PATH/TO/FILE.conf` with the actual path of your *.conf* wireguard file.

To learn more about wireguard configuration in NetworkManager, see: <https://blogs.gnome.org/thaller/2019/03/15/wireguard-in-networkmanager/>

## Thanks to

https://github.com/podobu/wifimenu  
https://github.com/nickclyde/rofi-bluetooth

## License

menus is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

menus is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.
 
You should have received a copy of the GNU General Public License along with this program. If not, see <https://www.gnu.org/licenses/>.
