# fan-supervisor-proxmox
Custom silent fan profile.

The script will check the CPU temperature ever 2 seconds.
Fans will be set to manual and low RPM unless the temperature reaches the `UPPER_TEMP` value.
Upon reaching the upper value, the iDRAC settings kick in and manual fan control is disabled.

## Prerequisite
For this to work, the script relies on the ipmitool binary.
Make sure to install the ipmitool
```
apt update
apt install ipmitool
```

## Customize and Install
Customizations can be applied to the scripts.

1. Update the `SENSOR_ID` value in the `start_fan_supervisor.sh` script.
To get your sensor id run this after installing the ipmitool.
```
ipmitool sdr type temperature
```
Sample output:
```
Inlet Temp		| 04h | ok  |  7.1 | 26 degrees C
Temp			| 0Eh | ok  |  3.1 | 49 degrees C
Temp			| 0Fh | ok  |  3.2 | 52 degrees C
```
Select the sensor id to be monitored and update the `SENSOR_ID` value.
2. Modify the scripts to your needs.
3. Copy the scripts and the service files in their appropriate directories
```
/opt/fan_supervisor/start_fan_supervisor.sh
/opt/fan_supervisor/stop_fan_supervisor.sh
/etc/systemd/system/fan_supervisor.service
```
4. Reload systemd
```
systemctl daemon-reload
```
5. Enable the service to start on boot
```
systemctl enable fan_supervisor
```
6. Start the service for current session or reboot
```
systemctl start fan_supervisor
```
