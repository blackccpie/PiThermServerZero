# PiThermServerZero

PiThermServer running on the Raspberry Pi Zero

## Installing PiThermServer

Follow [these](https://github.com/talltom/PiThermServer) instructions to deploy PiThermServer in your home directory.

## Autorunning PiThermServer

1. In your home directory, create a script called `start_temp_server.sh` with the following content:
```sh
#!/bin/sh

# time synchro
sudo /etc/init.d/ntp stop
sudo ntpd -q -g
sudo /etc/init.d/ntp start

sleep 10

# server start
cd /home/pi/PiThermServer
./build_database.sh
node server.js &
cd -
```

2. Open your `rc.local` file for edition:
```
$ sudo nano /etc/rc.local
```

3. Add the following line before the `exit 0` ending line:
```sh
sh /home/pi/start_temp_server.sh
```
