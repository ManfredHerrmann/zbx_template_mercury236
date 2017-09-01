# zbx_template_mercury236
Zabbix 'Template Pwr Mercury236' to monitor Mercury power meters using https://github.com/Shden/mercury236 utility app and JSON parsing in Zabbix 3.4.
# Requirements
Zabbix 3.4  

# Install and use

```
git clone https://github.com/Shden/mercury236.git
cd mercury236
make
cp mercury236 /etc/zabbix/scripts/
cd /etc/zabbix/scripts/
chmod +x mercury236
usermod -G dialout zabbix
#test run (assuming that /dev/ttyS0 is the RS485 port with PowerMeter attached to it:)
./mercury /dev/ttyS0 --json  
#observe the values received from PM.
```

Add to the configuration file of your Zabbix agent:
```
UserParameter=mercury236[*],/etc/zabbix/scripts/mercury236 $1 $2
```
And restart zabbix-agent:
`service zabbix-agent restart`


## In Zabbix
- Import template  
- Attach it to host with Zabbix agent  
- Change value of macro `{$SERIAL}` to serial port required if other than /dev/ttyS0  
