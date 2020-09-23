# Useful Commands

- Check specific FS: `df -h /boot`
- set global aliases: `sudo vi /etc/bashrc`
- `sudo su` - will put you into a root environment but it will ask you for your user password instead of the root password
- `su`: allows to tun commands with substitute user and group ID (without commands, root)
- `less /proc/meminfo` - ram size
- `free -m`: display global and swap memory usage
- `vmstat`: reports information about processes, memory, paging...
- `pmap <PID>`:
- debian: `sudo dpkg -i *.deb`
- In the command line `!$`: represents the last argument `cd dir1 || mkdir !$ && cd !$`
  - the `!v` returns the last command executed that started with **v**.
  - `vi +/install readme`: first instance of the word install on file readme.

## Diego Wisdom

```bash
+++++++++++++++++++++++++++++++++++++++++++
UXMONBROKER
+++++++++++++++++++++++++++++++++++++++++++
/var/opt/OV/bin/instrumentation/UXMONbroker -d psmon -c /var/opt/OV/conf/OpC/ps_mon.cfg -l /tmp/ps_mon.test
/var/opt/OV/bin/instrumentation/UXMONbroker -d dfmon -c /var/opt/OV/conf/OpC/df_mon.cfg -l /tmp/df_mon.test
/var/opt/OV/bin/instrumentation/UXMONbroker -d nicmon -c /var/opt/OV/conf/OpC/nic_mon.cfg -l /tmp/nic_mon.test

+++++++++++++++++++++++++++++++++++++++++++
```

## NTP en un server de ORACLE NO SE TOCA

## NTP alerts

- Ntpoffset
- ntpstat
- ntpq -p

## NTP en un server de ORACLE NO SE TOCA

## Too many instances

- ps -ef | grep http | wc -l
- Ps_mon.cfg
- Http
- Htttd 1-10
- Ps -ef | grep http
- Find /var -name ps_mon.cfg
- Locate ps.mon.cfg

## VMTOOLS not running

- ps -f | grep vm
- /etc/vmware-tools/services.sh status
- /etc/vmware-tools/services.sh restart
- /etc/vmware-tools/services.sh restart

## Event flow broken

- Server rebooted
- Agent disconected to hpom
  - Opcagt -status
  - Opcagt -restart
  - Opcagt -cleanstart

## FS

- du -sh <directory>

### TAR

- tar -zcvf <newFileName> <fileToCompress>
- tar -zxvf <file2Decompress>

## FAIL PATH VAR/LOG/MESSAGES

cat /var/log/messages # check messages containing errors

## UXMON: The number of Open LV and Current LV is different for VG: VolGroup00.

lvs
lvdisplay VolGroup00
