# Net

## PING
```bash
 ping -v4 dev.gid-msk.ru -c 3 -s 1400
```

#### Ping - max speed 
```bash
 ping -v4 dev.gid-msk.ru -c 125 -s 1400 -i 0.1 -f
```

## tracepath
```bash
tracepath linkmeup.ru
```

## mtr
```bash
mtr linkmeup.ru
```


## mtr - australian site
```bash
mtr 103.95.114.117 -T
```

## tcpdumbp
```bash
sudo tcpdump not port 22 -i any
```




