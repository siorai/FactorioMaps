# Factorio Maps
![image](https://user-images.githubusercontent.com/6313423/46447780-0d723880-c784-11e8-8e6f-2b35d24f25b9.png)
This [Factorio](http://www.factorio.com/) mod turns your factory into a timeline! You can view the map locally or upload it to a web server.

Live demo: https://factoriomaps.com/beta/user/L0laapk3/megabase/index.html

Mod portal link: https://mods.factorio.com/mod/L0laapk3_FactorioMaps

# How to Install
**Note that since version 3, this program now runs on python 3 instead of python 2.**
1. Download FactorioMaps to `%appdata%\mods\`, either from the [mod portal](https://mods.factorio.com/mod/L0laapk3_FactorioMaps) (The mod does not need to be enabled to work) and then unzipping it, or [downloading the git repo](https://github.com/L0laapk3/FactorioMaps/releases). 
1. Install the latest version of [python 3.7](https://www.python.org/downloads/). (Do not install python 2.)
1. Recommended: [Add python to your environment variables](https://stackoverflow.com/a/4855685/3185280).
1. Install pip: Download the latest [get-pip.py](https://bootstrap.pypa.io/get-pip.py), and run it (`python get-pip.py` in the command line).
1. Install the following pip packages: `pip install Pillow psutil`.

# How to Use
1. Make sure you close factorio before starting the process.
1. Navigate to the FactorioMaps folder (`%appdata%\Factorio\mods\FactorioMaps_x.x.x`). Unzip it if you haven't done that already.
1. Open a command line by typing cmd in the address bar and pressing enter. ![opening cmd](https://user-images.githubusercontent.com/6313423/46446227-6ab5bc00-c77b-11e8-982e-b040f964a778.png)
1. Run `python auto.py`. Some syntax examples:
    * `python auto.py` Generate a snapshot of the latest modified map (autosaves are excluded) and store it to a folder with the same name. If the folder already exists, the snapshot will be appended to the timeline.
    * `python auto.py savename` Generate a snapshot of *savename* and store it to folder *savename*.
    * `python auto.py outfolder savename` Generate a snapshot of *savename* and store it to folder *outfolder*.
    * `python auto.py outfolder savename1 savename2 savename3` Generate timeline snapshots of *savename1*, *savename2*, *savename3* in that order, and store it to folder *outfolder*.
    * `python auto.py --factorio=PATH` Same as `python auto.py`, but will use `factorio.exe` from *PATH* instead of attempting to find it in common locations.
    * `python auto.py --verbosegame` Display *all* game logs.
    * `python auto.py --basepath=PATH` Same as `python auto.py`, but will output to *PATH* instead of `script-output\FactorioMaps`. Not recommended to use.

1. An `index.html` will be created in `%appdata%\Factorio\script-output\FactorioMaps\mapName`. Enjoy!

# Configuration
Heres a list of flags that `auto.py` can accept:

| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;flag&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description |
| --- | --- |
| `--dayonly` | Do not take nighttime screenshots (For now, this setting needs to be the same across one timeline). |
| `--nightonly` | Do not take daytime screenshots. |
| `--hd` | Take screenshots of resolution 64 x 64 pixels per in-game tile instead of 32 x 32 to match the resolution of the newer HD textures. |
| `--no-altmode` | Hides entity info (alt mode) |
| `--build-range=5.2` | The maximum range from buildings around which pictures are saved (in chunks, 32 by 32 in-game tiles). |
| `--connect-range=1.2` | The maximum range from connection buildings (rails, electric poles) around which pictures are saved. |
| `--tag-range=5.2` | The maximum range from mapview tags around which pictures are saved. |
| `--factorio=PATH` | Use `factorio.exe` from *PATH* instead of attempting to find it in common locations. |
| `--modpath=PATH` | Use *PATH* as the mod folder. |
| `--basepath=PATH` | Output to `script-output\PATH` instead of `script-output\FactorioMaps`. |
| `--date=dd/mm/yy` | Date attached to the snapshot, default is today. |
| `--verbosegame` | Displays *all* game logs. |
| `--noupdate` | Skips the update check. |
| `--maxthreads=N` | Sets the number of threads used for all steps. By default this is equal to the amount of logical processor cores available. |
| `--cropthreads=N` | Sets the number of threads used for the crop step. |
| `--refthreads=N` | Sets the number of threads used for the crossreferencing step. |
| `--zoomthreads=N` | Sets the number of threads used for the zoom step. |
| `--screenshotthreads=N` | Set the number of screenshotting threads factorio uses. |
| `--screenshotqueuesize=N` | Set the size of the factorio screenshotting queue. Too high values may cause high RAM usage and I haven't found any benefits to high values so I recommend not changing this. |
| `--delete` | Deletes the output folder specified before running the script. |
| `--dry` | Skips starting factorio, making screenshots and doing the main steps, only execute setting up and finishing of script. |
 
Image quality settings can be changed in the top of `zoom.py`.

# Hosting this on a server
If you wish to host your map for other people to a server, you need to take into account the following considerations: (You can change these once in `index.html.template` and they will be used for all future snapshots.)
1. Of the files that this program generates, the files required to be hosted are:
    * `index.html`
    * `mapInfo.js`
    * All __images__ in `Images\`.
    * All files in `lib\`.
    All other files, including txt and other non-image files in `Images\`, are not used by the client. Some of them are temporary files, some of them are used as savestate to create additional snapshots on the timeline.

# Known limitations
* If you only have the steam version of factorio, steam will ask you to confirm the arguments everytime the script tries to start up. The popup window will sometimes not focus properly. Please press alt tab a couple of times until it shows up. The only way to get around this is to install the standalone version of factorio.
* If the program crashes while making a snapshot, it is very likely to leave timelines behind in a 'bricked' state and will probably mess up future snapshots. The easiest way is to simply start over and regenerate all the snapshots from old savefiles. If thats not a possibility, feel free to contact me on discord (L0laapk3#2010) or create an Issue, I'll do my best to help you out.
* Running this on headless servers is not possible due to factorio limitations.

# Issues
If you have problems or questions setting things up, feel free to reach out to me on discord at L0laapk3#2010.
If you believe you have found a bug, inconsistency, something unclear or anything else, please try generating a map to a new empty output folder (If you need help recovering bricked timelapses, please reach out to me). If the problem persists, please submit an issue to the [Issue tracker](https://github.com/L0laapk3/FactorioMaps/issues).
