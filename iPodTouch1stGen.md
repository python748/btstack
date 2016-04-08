# Introduction #

The BTstack package in Cydia does not support the iPod Touch 1st gen, as it has to be configured for the used external Bluetooth module. For this to work, you need an iPod Connector and an 3.3V Bluetooth module with a UART/H4 interface, e.g. the Mitsumi WML-C09 or the Rayson BTM-330. [More info on the external Bluetooth module for iPod](http://www.ubiqkom.org/blog/?p=38).

# Details #
Configure build system for THEOS/iOS builds
```
./config-iphone.sh
```

Configure BTstack daemon to use dev/tty.iap instead. It should use hci\_transport\_h4.c instead of hci\_transport\_h4\_iphone.c

Disable flow control in src/daemon.c, line 250:
From
```
config.flowcontrol = 1;
```

into
```
config.flowcontrol = 0;
```

Then, compile and build package
```
make package
```

The resulting .deb can be installed with "dpkg -i BTstack-0.1-xxx.deb" on the iPod Touch. Try the "inquiry" command!