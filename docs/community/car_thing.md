# Spotify CarThing

!!! note
    This guide is written and provided by TechGeek01, after modifying two of his own units.
    The information is from multiple sources and is compiled in a way that worked for him. Your mileage may vary.
    Proceed with caution, and be mindful of your actions.

!!! warning
    I've tested this on Windows. Guides for Linux and Mac are copied from my references, and I have not tested them. ***Fuck your shit up at your own risk.***
    
    The instructions for Windows are what worked for me. I'll also assume syntax for Windows, and use backslashes and Windows syntax for the commands. Adjust accordingly if you're not using Windows.

# Download all the things
- [Zadig 2.9](https://zadig.akeo.ie/)
- Thing Labs firmware from [thingify.tools](https://thingify.tools/) - Currently 8.9.2
- [thinglabsoss/superbird-tool](https://github.com/thinglabsoss/superbird-tool) on GitHub - Click the green dropdown and download the ZIP archive of the code
- [Git](https://git-scm.com/downloads)
- [Python](https://www.python.org/) - I'm using 3.12. Officially, Superbird docs say it's tested with 3.10 and 3.11, but 3.12 worked for me.

1. Extract Superbird to anywhere you like. I'll assume you've called it `superbird`
2. Extract your Thing Labs firmware to a folder inside of `superbird`. I'll assume you've called this `thinglabs`. This folder should have all the data files directly inside of it

# Setting up to fuck around
Before we fuck around, you need the right drivers.
1. If your Car Thing is plugged into your PC, unplug that shit
2. Hold down buttons 1 and 4
3. While holding them, plug it in. If this is done correctly, your PC should see it, but the screen will remain blank, and it won't try to boot with the regular boot process.
4. If you did this correctly, Zadig should show you a `GX-CHIP` device. The driver you want is *generally* `libusb`. On Windows specifically, you want `libusbK` instead.
5. Install the driver

# Fucking around
Before you can do anything with the Car Thing, modified firmware has to be flashed. Without this, things like ADB and such aren't exposed.

At this point, I'll assume a few things:
1. You have the correct `libusb` or `libusbK` driver installed
2. You've extracted Superbird to the `superbird` directory
3. You've extracted the Thing Labs firmware to the `superbird\thinglabs` directory
Get your happy ass a command prompt, terminal, or whatever shell window you like, and get to `superbird` wherever it is that you put it.

1. If your Car Thing is plugged in still, unplug that shit
2. The same as before, hold buttons 1 and 4
3. While still holding those buttons, plug it in
## Python requirements
### Windows
```
python -m pip install git+https://github.com/superna9999/pyamlboot
python -m pip install pyusb
python -m pip install libusb
```
### Linux
!!! warning
    ***I haven't tested this. This is copied and pasted from Superbird docs.***

> On Linux, you just need to install pyamlboot. However, `root` is needed on Linux, unless you fiddle with udev rules, which means the pip package also needs to be installed as `root`

```
sudo python3 -m pip install git+https://github.com/superna9999/pyamlboot
```
### macOS
!!! warning
    ***I haven't tested this. This is copied and pasted from Superbird docs.***

> On macOS, you must install `python3` and `libusb` from homebrew, and execute using that version of python

```
brew install python3 libusb
/opt/homebrew/bin/python3 -m pip install git+https://github.com/superna9999/pyamlboot
```

## Continuing to fuck around
If this all worked correctly, running
```
superbird_tool.py --find_device
```

Should show you something like `Found device booted in USB Mode`.

To enter burn mode, run
```
superbird_tool.py --burn_mode
```

Once you're successfully in burn mode, it's time to flash the modded firmware.

```
superbird_tool.py --restore_device ./thinglabs
```

This is gonna take a few minutes, but if all goes well, you should have modded firmware now.

!!! note
    **If this fails for you on Windows with something like `KeyError` or something about amlmmc env, it's probably because you installed the `libusb` driver instead of `libusbK`.** If this is the case, unplug the Car Thing, plug it back in while holding buttons 1 and 4 to boot in USB mode, go back into Zadig if this is the case, and reinstall the `libusbK` driver instead.

Unplug your Car Thing and plug it back in to drop out of USB mode, and boot normally. If all goes well, you should see the "ThingLabs" logo on boot.

# Doing shit with the Car Thing
The 2 things I've tested are DeskThing and GlanceThing. I prefer the layout of DeskThing in general, as it's closer to stock Spotify for media stuff, but personally, it seems to lag behind for me on media updates. I find GlanceThing to be smoother of a process. I'll outline the process I followed for both.

## DeskThing
Download DeskThing Server from [ThingLabs](https://thingify.tools/firmware/aKYXqc_4TE-hv8Q1Khr7F?tab=versions) and install it. When you're done, run it.

1. Under the "Clients" tab, you *should* see your Car Thing in the list. If it fails to connect, try clicking the "configure" button to connect it.
2. On the "Downloads" tab, find and download the "Spotify" app.
    1. Once it finishes, click "Initialize App"
3. Go to the "Apps" tab, and click the bubble that says "Requesting Data", and follow the directions to go to the Spotify dev dashboard and create your app.
    1. Copy and paste in the client ID and client secret when DeskThing asks, which is how this will connect to Spotify's API.
    2. Set the endpoint url to `http://localhost:8888/callback/spotify`
    3. Save, and you should see a browser window pop up with a success message. You can close that Window.

## GlanceThing
Download the latest version of GlanceThing from the [releases page](https://github.com/BluDood/GlanceThing/releases) on GitHub and install it.

GlanceThing will guide you through the install process, and is a lot easier to install than DeskThing.

Rather than use the API, GlanceThing *currently* uses a token from open.spotify.com, which it guides you through obtaining and providing, so that it can pull the now playing data.

!!! note
    ***GlanceThing runs in memory, and doesn't perma install like DeskThing does.*** Instead of opening GlanceThing on your computer every time you plug in the Car Thing, and reinstalling, you can click on the cog in the top right of GlanceThing, and toggle the auto install option. This will auto reinstall GlanceThing every time it sees a Car Thing that doesn't have it running, so you don't have to load it into memory every boot.