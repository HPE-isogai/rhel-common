https://access.redhat.com/documentation/ja-jp/red_hat_enterprise_linux/7/html/system_administrators_guide/ch-configuring_ntp_using_ntpd

1. install ntp
```
yum install ntp
```

2. Configure ntp.conf
```
# cat /etc/ntp.conf |grep -v ^# |grep -v ^$
driftfile /var/lib/ntp/drift
restrict default nomodify notrap nopeer noquery
restrict 127.0.0.1
restrict ::1
server 16.110.135.123 iburst  #Set IP address as your environment
includefile /etc/ntp/crypto/pw
keys /etc/ntp/keys
disable monitor
minpoll 2 and maxpoll 6  # Add this line if you want sync frequently
```

3. start ntpd
```
systemctl enable ntpd
systemctl restart ntpd
```

```
# systemctl status ntpd
● ntpd.service - Network Time Service
   Loaded: loaded (/usr/lib/systemd/system/ntpd.service; enabled; vendor preset: disabled)
   Active: active (running) since Fri 2021-03-19 03:51:48 EDT; 4s ago
  Process: 28221 ExecStart=/usr/sbin/ntpd -u ntp:ntp $OPTIONS (code=exited, status=0/SUCCESS)
 Main PID: 28222 (ntpd)
   CGroup: /system.slice/ntpd.service
           └─28222 /usr/sbin/ntpd -u ntp:ntp -g

Mar 19 03:51:48 transproxy ntpd[28222]: Listen normally on 2 lo 127.0.0.1 UDP 123
Mar 19 03:51:48 transproxy ntpd[28222]: Listen normally on 3 ens192 15.210.188.131 UDP 123
Mar 19 03:51:48 transproxy ntpd[28222]: Listen normally on 4 ens224 10.0.255.254 UDP 123
Mar 19 03:51:48 transproxy ntpd[28222]: Listen normally on 5 lo ::1 UDP 123
Mar 19 03:51:48 transproxy ntpd[28222]: Listen normally on 6 ens192 fe80::2357:32fd:c61d:9e06 UDP 123
Mar 19 03:51:48 transproxy ntpd[28222]: Listen normally on 7 ens224 fe80::f3:733f:1d33:f4e9 UDP 123
Mar 19 03:51:48 transproxy ntpd[28222]: Listening on routing socket on fd #24 for interface updates
Mar 19 03:51:48 transproxy ntpd[28222]: 0.0.0.0 c016 06 restart
Mar 19 03:51:48 transproxy ntpd[28222]: 0.0.0.0 c012 02 freq_set kernel 0.000 PPM
Mar 19 03:51:48 transproxy ntpd[28222]: 0.0.0.0 c011 01 freq_not_set
```


## Client side confirmation
### Common
```
$ timedatectl
```

### Chrony
```
$ chronyc tracking
$ chronyc sources
```
