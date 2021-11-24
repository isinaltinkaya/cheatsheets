####

### - If you somehow managed to destroy your dns resolver and missing the `/etc/resolv.conf`

First go to the nearest collegue and ask to use their terminal. Ping to the archive of your OS to obtain the IP address.

`ping archive.ubuntu.com`

Then using your terminal
```
sudo vim /etc/hosts
```

Add the IP to the hosts in this format
```
X.X.X.X\tarchive.ubuntu.com
```
e.g.
```
81.189.88.142 archive.ubuntu.com
```
