# youtube-dmenu
Your Youtube subscriptions in dmenu

## Instructions
First off download your Youtube subscriptions from the bottom of this page https://www.youtube.com/subscription_manager and save the file somewhere.
This file does not update automaticly so if you change your subscriptions on the site you have to redownload it.

The following instructions expect that path to your `subscription_manager` file is `~/subscription_manager` and both `updateytsubs` and `selectytvideo` are located in `~/.scripts/` folder.

Running `updateytsubs` list all your subscription video details to `~/.youtubesubs`.
You must give it path to the `subscription_manager` as the first argument.
It is best to create a cronjob for this. For example to update every 15 minutes run `crontab -e` and add something on the lines of:
```
*/15 * * * * ~/.scripts/updateytsubs ~/subscription_manager
```

`selectytvideo` reads the `~./youtubesubs` file and lets you to select one using dmenu.
It returns the video url that you can use as a parameter for your favourite media player.
For example if using mpv:
```
mpv -fs "$(~/.scripts/selectytvideo)"
```
If you are using i3 wm I recommend adding the following to your i3/config:
```
bindsym $mod+y exec mpv -fs "$(~/.scripts/selectytvideo)"
```

