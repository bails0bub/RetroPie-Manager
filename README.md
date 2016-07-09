# Retropie-Manager
Recalbox-Manager fork for RetroPie 4.x

![alt tag](https://github.com/botolo78/RetroPie-Manager/blob/retropie/screenshot.png)

# About

This a Recalbox-Manager fork aimed to be used with RetroPie 4.x **running on Raspberry Pi**.

Original repository: https://github.com/recalbox/recalbox-manager

# Features
With Retropie-Manager you can
- Monitor the raspberry health and disk space
- Edit the Emulation Station config file
- Edit the RetroArch config file
- Edit the autostart.sh script
- View the Emulation Station log file
- Manage your BIOS files
- Manage your ROMS

# Limitations

- In this release the virtual gamepad page has been removed.
- It is tested in Raspberry Pi. Some users reported problems to install it on an ubuntu-based RetroPie installation (the ubuntu repositories don't have the virtualenv package).
- It doesn't support subdirectories at ROMs dir (as reported [here](https://github.com/botolo78/RetroPie-Manager/issues/5))


# Install
```sh
sudo apt-get install virtualenv python-dev
```

```sh
cd
git clone https://github.com/botolo78/RetroPie-Manager.git
cd RetroPie-Manager
make install
```

# Usage

You must be at the RetroPie-Manager's directory to use the `rpmanager.sh` like in the examples below.

**Start**
```sh
./rpmanager.sh --start
```
Open your browser and go to **http://your_retropie_ip:8000/**

**Stop**
```sh
./rpmanager.sh --stop
```

**More options**
```sh
[prompt]$ ./rpmanager.sh --help
Usage: rpmanager.sh OPTIONS

The OPTIONS are:

-h|--help           print this message and exit

--start             start the RetroPie-Manager

--stop              stop the RetroPie-Manager

--isrunning         show if RetroPie-Manager is running and the
                    listening port and exit

--log               save the log messages (optional, default: not save log
                    messages, only works with --start)

-u|--user USER      start RetroPie-Manager as USER (only available for
                    privileged users, only works with --start, USER must 
                    be a RetroPie user)

The --start and --stop options are, obviously, mutually exclusive. If the
user uses both, only the first works.

```


# Autostart
To make Retropie-Manager to start with your raspberry edit your autostart.sh

```sh
sudo nano /opt/retropie/configs/all/autostart.sh
```
and add this command before **emulationstation #auto** [replace `/PATH/TO/` with the RetroPie-Manager's full path, and `RETROPIE_USER` with the RetroPie username, it's usually `pi` on a Raspberry Pi.]

```sh
/PATH/TO/RetroPie-Manager/rpmanager.sh --start --user RETROPIE_USER 2>&1 &
```

# Update
```sh
sudo kill -9 $(pgrep -f RetroPie-Manager)
cd 
cd Retropie-Manager
make clean
git reset --hard HEAD
git pull
make install
```

# Reinstall
```sh
sudo kill -9 $(pgrep -f RetroPie-Manager)
cd 
rm -rf Retropie-Manager
git clone https://github.com/botolo78/RetroPie-Manager.git
cd RetroPie-Manager
make install
```

# Known bugs

- (FIXED) You'll get a 404 error trying to delete roms
