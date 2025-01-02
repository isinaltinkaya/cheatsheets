# Use iPad as second monitor: Arch Linux edition

## 1) Find your IP address

```
IPADDR=$(ip addr show | grep -E '^\s*inet' | grep -m1 global | awk '{ print $2 }' | sed 's|/.*||')
```

## 2) Set the IP address on your iPad/VNC app

Use `IPADDR:5900` as the address.

## 3) Run the following script

```
bash ipad_monitor.sh
```

Get `ipad_monitor.sh` from https://kbumsik.io/using-ipad-as-a-2nd-monitor-on-linux

