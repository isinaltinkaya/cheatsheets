### Permission management


```
for i in `find PATH/ -type d`;do USR=$(stat -c "%U" $i); sudo runuser -l ${USR} -c "chmod 777 ${i}";done
```
