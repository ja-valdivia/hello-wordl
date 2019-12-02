# Feature 7898: Fault and Performance Management of OSM Modules

This feature enables a graphical interface of the OSM components using the prometheus operator and the graphical grafana
web interface


## Prerequisites

It is needed to install OSM with kubernetes

* Presto-SDK.zip (https://mef.box.com/s/h5j78genqwx2y4z7msho6119wxqnpffe)
* Presto-SDK.z01 (https://mef.box.com/s/2rhbl3ct3wqkszm06ootbe31frjhyhps)

Login: mef-dev
Password: mef-dev

Here are the commands to unzip after you have downloaded both the files

* zip -s 0 Presto-SDK.zip --out Presto-SDK-full.zip
* unzip Presto-SDK-full.zip

Alternatively, you can install mininet and Opendaylight by yourself. Presto SDK R2 is not
part of official distribution of Opendaylight yet, but you can download the sources from 
this GitHub fork: https://github.com/donaldh/unimgr/tree/presto-20180307  

If you need to manually start OpenDaylight, these are the steps:

### Start OpenDaylight

```sh
% cd unimgr-karaf-0.3.1.SNAPSHOT
% ./bin/karaf
Apache Karaf starting up. Press Enter to open the shell now...
100% [========================================================================]

Karaf started in 17s. Bundle stats: 338 active, 338 total

    ________                       ________                .__  .__       .__     __
    \_____  \ ______   ____   ____ \______ \ _____  ___.__.|  | |__| ____ |  |___/  |
     /   |   \\____ \_/ __ \ /    \ |    |  \\__  \<   |  ||  | |  |/ ___\|  |  \   __\
    /    |    \  |_> >  ___/|   |  \|    `   \/ __ \\___  ||  |_|  / /_/  >   Y  \  |
    \_______  /   __/ \___  >___|  /_______  (____  / ____||____/__\___  /|___|  /__|
            \/|__|        \/     \/        \/     \/\/            /_____/      \/


Hit '<tab>' for a list of available commands
and '[cmd] --help' for help on a specific command.
Hit '<ctrl-d>' or type 'system:shutdown' or 'logout' to shutdown OpenDaylight.

opendaylight-user@root>
```
