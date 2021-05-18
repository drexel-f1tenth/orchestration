# orchestration

Managing ROS nodes with systemd services

## Service Units

- `racecar`: This service unit serves as a group for managing the other services. So, for example, running `sudo sysemctl start racecar` will start all of the following services as well.
- `racecar-roscore`: This service manages the `roscore` nodes.
- `racecar-lidar`: This service manages the ROS node for the LiDAR module.
- `racecar-mcu`: This service manages the ROS node for the motor control unit.
- `racecar-pathfinder`: This service manages the pathfinder node.

## Installation

- `sudo cp service-units/*.service /etc/systemd/system/`
- `sudo cp service-units/*.sh /usr/local/sbin/`
- `sudo systemctl daemon-reload`
- `sudo systemctl enable racecar racecar-roscore racecar-lidar racecar-mcu racecar-pathfinder`

## Useful commands

- View logs using `journalctl` (follow with the `-f` option)
- Check status of all nodes: `sudo systemctl status racecar*`
- Stop a service: `sudo systemctl stop ${service-name}`
- Start a service: `sudo systemctl start ${service-name}`
- Restart a service: `sudo systemctl restart ${service-name}`
