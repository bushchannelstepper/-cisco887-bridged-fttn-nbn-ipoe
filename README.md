Cisco config for 877VA-M for use in bridged mode with Aussie Broadband
======================================================================

Note that you'll need updated VDSL firmware since the boxes were manufactured for this to work.  Mine shipped with this so I haven't had to chase it up, but there are conversations on whirlpool about it if you need.

To configure from a Mac using Aten UC-232A USB to serial convertor:

Install latest Mac OS driver for Aten UC-232A
Allow kernel extension in security preferences, run the installer again, reboot again (tested with Mojave and Catalina)

```
% ls -l /dev|grep 232
crw-rw-rw-  1 root  wheel           18,   1 21 Oct 13:28 cu.UC-232AC
crw-rw-rw-  1 root  wheel           18,   0 21 Oct 13:30 tty.UC-232AC
% screen /dev/tty.UC-232AC

crisco>
```

Woo!

Reset config to default:
------------------------

If that seems like a good idea.

https://www.hardreset99.com/routers/cisco/cisco-887va-factory-reset/

```
router > enable
router# write erase
Erasing the nvram filesystem will remove or format all configuration files! Continue? [confirm] < Press Enter key >
router# reload
```

'no' to initial setup configuration

power off and cold boot to default


Let's install our config:
-------------------------

```
crisco>enable
crisco#configure terminal
[PASTE YOUR CONFIG IN HERE then HIT ENTER]
crisco#write mem
```

You can reboot here.

A few handy commands:

```
crisco#show controller vdsl 0
crisco#show ip int bri
crisco#show run brief
```

`show controller vdsl 0` should let you know how the modem sync is going.  It takes 5-10 mins with VDSL2.

Forward to your router's WAN input from any of the FastEthernet ports.  Except FastEthernet2 which should allow router access via telnet on 192.168.211.211.

20191021 800m line length from the green box:

Attainable Rate:        54379 kbits/s            13212 kbits/s

No thanks to the hacks who dreamt up "MTM".