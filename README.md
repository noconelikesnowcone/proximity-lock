# Proximity lock

Lock the screen when a chosen phone or watch leaves Bluetooth range.

You pick the device once. The watcher arms after it has seen that device nearby. When the device stays silent, a warning appears, then the screen locks. Coming back does not unlock the screen. A Bluetooth outage on the computer does not lock it.

Apple devices rotate their Bluetooth address, so the phone or watch has to be paired. After pairing, BlueZ follows that device.

The picker uses the Omarchy menu. The lock uses `omarchy system lock`, and falls back to `loginctl lock-session`.

## Install

```bash
git clone https://github.com/noconelikesnowcone/proximity-lock.git
cd proximity-lock
install -Dm755 proximity-lock ~/.local/bin/proximity-lock
install -Dm644 proximity-lock.desktop ~/.local/share/applications/proximity-lock.desktop
proximity-lock pick
```

`pick` scans, asks you to choose, pairs the device, and starts a user service. The chosen device is stored in `~/.config/proximity-lock/config.json`.

Needs BlueZ, `python-dbus`, `python-gobject`, `notify-send`, and Omarchy.

## Use

```bash
proximity-lock status
proximity-lock pause          # hold until resume
proximity-lock pause 30       # hold for 30 minutes
proximity-lock resume
proximity-lock off
proximity-lock on
proximity-lock forget         # stop watching and remove the pairing
```

Open **Proximity lock** from the app launcher to pick a different device.

The screen locks after the device has been silent for 20 seconds, then a 6 second warning. Change `away_seconds` and `warn_seconds` in the config file and run `proximity-lock on` again.

## License

MIT. See [LICENSE](LICENSE).
