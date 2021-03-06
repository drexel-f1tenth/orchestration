# orchestration

Managing ROS nodes with systemd services

## Service Units

- `racecar`: This service unit serves as a group for managing the other services. So, for example, running `sudo sysemctl start racecar` will start all of the following services as well.
- `racecar-roscore`: This service manages the `roscore` nodes.
- `racecar-lidar`: This service manages the ROS node for the LiDAR module.
- `racecar-mcu`: This service manages the ROS node for the motor control unit.
- `racecar-pathfinder`: This service manages the pathfinder node.

## Installation

The Ubuntu Modem Manager must be disabled, since it has a long init process which makes the device on /dev/ttyACM0 fail to startup on boot, because it is not a modem:

`sudo systemctl disable ModemManager.service`

Setup the orchestration services:
- `sudo cp service-units/*.service /etc/systemd/system/`
- `sudo cp service-units/*.sh /usr/local/sbin/`
- `sudo systemctl daemon-reload`
- `sudo systemctl enable racecar racecar-roscore racecar-lidar racecar-mcu racecar-pathfinder`

## Useful commands

- View logs: `journalctl -fu ${service-name}`
- Check status of all nodes: `sudo systemctl status racecar*`
- Stop a service: `sudo systemctl stop ${service-name}`
- Start a service: `sudo systemctl start ${service-name}`
- Restart a service: `sudo systemctl restart ${service-name}`
