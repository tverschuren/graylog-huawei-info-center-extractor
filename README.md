# Graylog Extractor for huawei AR Routers Info-center / Syslog

### First a note
In huawei info-center you cannot specify a tcp/udp port for sending messages to.
As a work-around we create a NAT rule on the Ubuntu server where graylog is.

This only works if no other devices send syslog to UDP/514.

`iptables -t nat -A PREROUTING -i eth0 -p udp --dport 514 -j REDIRECT --to-port 11002`

(You can run graylog as root to let it listen directly on port 514, then you would not need this NAT rule, but that's not recommended)

### Huawei router config
The router(s) are configured like this

```
info-center enable
info-center loghost [IP ADDRESS] transport udp
```

### Message
The raw message looks like this
`<189>Dec  8 2016 07:02:39 4GT-MYHOSTNAME %%01SHELL/5/CMDRECORD(l)[31]:Record command information. (Task=Co0, Ip=**, User=admin, Command="log on", Result=Success)`

After the extractor it looks like this
![Alt](/screenshot.png "graylog_screenshot")
