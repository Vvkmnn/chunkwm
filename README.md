# vWindowDaemon

A preservative fork of one of my favorite window managers. [chunkwm](https://github.com/koekeishiya/chunkwm). All credit goes to the original author(s).

### Building

On macOS `10.13.1`:

Requires xcode-8 command line tools.

```sh
git clone https://github.com/vvkmnn/vWindowDaemon.git
cd vWindowDaemon
git pull remote upstream
```

#### chunkwm-core
The underlying logic that abstracts window management.

```sh
cd chunkwm
make install
cp bin/chunkwm /usr/local/bin
# cp examples/chunkwmrc ~/.chunkwmrc
# cp examples/com.koekeishiya.chunkwm.plist ~/Library/LaunchAgents
```

#### chunkc
A little shell script 'daemon' that runs in the background to listen for events.

```sh
cd chunkwm/src/chunkc
make
cp bin/chunkc /usr/local/bin
```

#### chunkwm-tiling:
A plugin that manages the tiling and binary split behavior.

```sh
cd chunkwm/src/plugins/tiling
make install
mkdir -p ~/.chunkwm_plugins
cp ../../../plugins/tiling.so ~/.chunkwm_plugins
```

#### chunkwm-border
A plugin that allows us to highlight certain windows. 

```sh
cd chunkwm/src/plugins/border
make install
mkdir -p ~/.chunkwm_plugins
cp ../../../plugins/border.so ~/.chunkwm_plugins
```

#### chunkwm-ffm
Focus-follows-mouse! The secret killer feature of this wm; start typing into windows on focus, and grab the mouse too!

```sh
cd chunkwm/src/plugins/ffm
make install
mkdir -p ~/.chunkwm_plugins
cp ../../../plugins/ffm.so ~/.chunkwm_plugins
```

### Setting

`chunkwm` uses a shell script as its configuration file and look for it at `$HOME/.chunkwmrc` (and needs to be executable via `chmod +x ~/.chunkwmrc`.  

A different location can be specified with the `--config | -c` argument.

The valid config-options for chunkwm-core are as follows:

```
chunkc core::log_file </path/to/log/file>
chunkc core::log_level <none | debug | warn | error>
chunkc core::plugin_dir </path/to/plugins>
chunkc core::hotload <1 | 0>
chunkc core::load <plugin>
chunkc core::unload <plugin>
```

Plugins can be loaded and unloaded at any time, without having to restart chunkwm.

Also depends on a little keyboard daemon to listen to keystrokes, which hands off to this daemon; I prefer the matching [skhd](https://github.com/koekeishiya/skhd), which I've also forked as [vHotkeyDaemon](https://github.com/Vvkmnn/vHotkeyDaemon).
