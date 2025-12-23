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

##IP - to find diveces in my sub-net

```bash
sudo arp-scan --localnet
```

```bash
ip address
```

### default via - for ex: 192.0.0.7 - the ip which PC went to internet
```bash
ip route
```

### JSON data
```bash
ip route  -j route | jq
ip route -4 -j route | jq
ip route -6 -j route | jq
ip route  -j address | jq
```


