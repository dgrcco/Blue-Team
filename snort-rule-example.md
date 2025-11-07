# Snort Alert Rule Example

Thread actor IP: 192.168.163.130 (VM)

Snort IP: 192.168.163.128 (VM)

Rule Options: [https://docs.snort.org/rules/options/](https://docs.snort.org/rules/options/)

## ICMP Ping Echo Request:

ICMP Protocol: [https://it.wikipedia.org/wiki/Internet_Control_Message_Protocol](https://it.wikipedia.org/wiki/Internet_Control_Message_Protocol)

```
alert icmp 192.168.163.130 any -> $HOME_NET any
(
        msg:"icmp echo request";
        itype:8; # ICMP Type 8 = Echo Request (Ping)
        dsize:>=0; # Packet must contain data
        sid:1000001; # rule id
        rev:1;
)
```

```
┌──(kali㉿kali)-[~]
└─$ ping 192.168.163.128
PING 192.168.163.128 (192.168.163.128) 56(84) bytes of data.
64 bytes from 192.168.163.128: icmp_seq=1 ttl=64 time=0.389 ms
64 bytes from 192.168.163.128: icmp_seq=2 ttl=64 time=0.427 ms
```

```
11/07-18:04:20.264022 [**] [1:1000001:1] "icmp echo request" [**] [Priority: 0] {ICMP} 192.168.163.130 -> 192.168.163.128
11/07-18:04:21.266913 [**] [1:1000001:1] "icmp echo request" [**] [Priority: 0] {ICMP} 192.168.163.130 -> 192.168.163.128
```

## SSH Bruteforce

```
alert tcp 192.168.163.130 any -> $HOME_NET 22
(
        msg:"ssh bruteforce";
        flow:established,to_server;
        content:"SSH",nocase,offset 0,depth 4;
        detection_filter:track by_src,count 5,seconds 60; # https://docs.snort.org/rules/options/post/detection_filter
        sid:2000002; # rule id
        rev:1;
)
```

```
┌──(kali㉿kali)-[~]
└─$ hydra -L user.txt -P psw.txt 192.168.163.128 ssh
```

```
11/07-18:05:52.730261 [**] [1:4000004:1] "ssh bruteforce" [**] [Priority: 0] {TCP} 192.168.163.130:51990 -> 192.168.163.128:22
11/07-18:05:52.743968 [**] [1:4000004:1] "ssh bruteforce" [**] [Priority: 0] {TCP} 192.168.163.130:52038 -> 192.168.163.128:22
```
## TCP SYN-FLOOD

```
alert tcp 192.168.163.130 any -> $HOME_NET 80
(
        msg:"possible tcp-syn flood";
        flags:S;
        dsize:0;
        detection_filter:track by_src,count 50,seconds 10;
        sid:6000006;
        rev:1;
)
```

```
sudo hping3 -S -p 80 192.168.163.128 -i u1000
```

```
11/07-18:32:53.834645 [**] [1:6000006:1] "possible tcp-syn flood" [**] [Priority: 0] {TCP} 192.168.163.130:2533 -> 192.168.163.128:80
11/07-18:32:53.876447 [**] [1:6000006:1] "possible tcp-syn flood" [**] [Priority: 0] {TCP} 192.168.163.130:2534 -> 192.168.163.128:80
```

## TCP ACK-FLOOD

```
alert tcp 192.168.163.130 any -> $HOME_NET 80
(
        msg:"possible tcp-ack flood";
        flags:A;
        dsize:0;
        detection_filter:track by_src,count 50,seconds 10;
        sid:7000007;
        rev:1;
)
```

```
sudo hping3 -A -p 80 192.168.163.128 -i u1000
```

```
11/07-18:54:47.075285 [**] [1:7000007:1] "possible tcp-ack flood" [**] [Priority: 0] {TCP} 192.168.163.130:1752 -> 192.168.163.128:80
11/07-18:54:47.136980 [**] [1:7000007:1] "possible tcp-ack flood" [**] [Priority: 0] {TCP} 192.168.163.130:1753 -> 192.168.163.128:80
```
