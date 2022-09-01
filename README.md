# Zabbix templates

## dehydrated-certs

Template for checking validity and expiration of SSL certificates obtained
using dehydrated - https://dehydrated.io/

Installation:

1. Put scripts in /etc/zabbix/scripts or whatever path you are using for your
   Zabbix Agent scripts. The script assumes /var/lib/dehydrated/certs as a
   location of certificates, if you use different path you must change in
   script code.
2. Put config file in /etc/zabbix/zabbix_agentd.conf.d or whatever path you
   are using for your custom Zabbix Agent configuration. Configuration
   assumes /etc/zabbix/scripts as script location. If you use different path
   you must change it in config file.
3. Import template into Zabbix and assign it to selected hosts.

All certificates will be automatically discovered and will be checked for
validity and expiration.

## disk-smart

Template for checking S.M.A.R.T. status of physical disks

Installation:

1. This template uses smartmontools - https://www.smartmontools.org/
   Be sure to install it before using this template.
2. Put script in /etc/zabbix/scripts or whatever path you are using for your
   Zabbix Agent scripts.
3. Put config file in /etc/zabbix/zabbix_agentd.conf.d or whatever path you
   are using for your custom Zabbix Agent configuration. Configuration
   assumes /etc/zabbix/scripts as script location. If you use different path
   you must change it in config file.
4. Import template into Zabbix and assign it to selected hosts.

All physical disks will be automatically discovered using /sys/block/*
entries and selected (pre-fail) S.M.A.R.T. attributes will be monitored.

## md-raid

Template for checking status of MD RAID arrays

Installation:

1. Put script in /etc/zabbix/scripts or whatever path you are using for your
   Zabbix Agent scripts.
2. Put config file in /etc/zabbix/zabbix_agentd.conf.d or whatever path you
   are using for your custom Zabbix Agent configuration. Configuration
   assumes /etc/zabbix/scripts as script location. If you use different path
   you must change it in config file.
3. Import template into Zabbix and assign it to selected hosts.

All MD RAID arrays will be automatically discovered using /sys/block/md*
entries and status of each array will be monitored (degraded status and
array sync status).

## ssl-certs

Template for checking validity and expiration of SSL certificates

1. Put scripts in /etc/zabbix/scripts or whatever path you are using for your
   Zabbix Agent scripts. The ssl_cert_list script assumes /etc/zabbix/scripts
   as a location of SSL service list file. If you use different path you must
   change in script code. The ssl_cert_check script was taken from
   https://github.com/selivan/https-ssl-cert-check-zabbix
2. Put config file in /etc/zabbix/zabbix_agentd.conf.d or whatever path you
   are using for your custom Zabbix Agent configuration. Configuration
   assumes /etc/zabbix/scripts as script location. If you use different path
   you must change it in config file.
3. Create list of SSL services to monitor in file ssl_cert_check.list under
   /etc/zabbix/scripts or whatever path you've set in ssl_cert_list script.
   Here is an example content of SSL service list file:

```
# My web server
my.server.com 443
# My FTP server over TLS
my.server.com 21/ftp
# My SMTP server over TLS
my.mail.server.com 25/smtp
# My SMTP server over SSL
my.mail.server.com 465
```

4. Import template into Zabbix and assign it to selected hosts.

All configured services and certificates will be automatically discovered and
will be checked for validity and expiration.

## sysv-services

Template for checking status of system services managed by SysV init system

Installation:

1. Put script in /etc/zabbix/scripts or whatever path you are using for your
   Zabbix Agent scripts.
2. Put config file in /etc/zabbix/zabbix_agentd.conf.d or whatever path you
   are using for your custom Zabbix Agent configuration. Configuration
   assumes /etc/zabbix/scripts as script location. If you use different path
   you must change it in config file.
3. Import template into Zabbix and assign it to selected hosts.

All system services will be automatically discovered using either chkconfig
command or entries in rc*.d directories. Only scripts for runleves 2 to 5
are being discovered and monitored. To exclude some service from discovery
and monitoring, create file sysv_services.excludes under /etc/zabbix/scripts
and list each service to be excluded, one per line. If you use different path
for Zabbix Agent scripts you must change it in script code.
