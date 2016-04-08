# Introduction #

On this page, we provide a quick walk-through to run example/l2cap-test.c on an iPhone/iPod/iPad and connect to a WiiMote, while displaying acceleration and button reports. See below for iPhone simulator usage.

# Requirements #
  * Xcode 4.4.1 installed at /Applications/Xcode-4.4.1.app
  * Xcode 5. Make sure xcode-select --print-path points to it
  * rpetrich's fork of the theos buid system from https://github.com/rpetrich/theos.git . Please set THEOS to the path of your theos installation/checkout
  * the ldid code-signing tool, either on your host or on the iPhone (via Cydia). If you install it on the build system, the signing is done automatically.
  * a subversion client
  * a jailbroken iPhone/iPod/iPad.

# Steps to compile and run a BTstack example on the iPhone #
  1. Install the BTstack package in Cydia
  1. get the BTstack project from the Google code SVN:
> > `svn checkout http://btstack.googlecode.com/svn/trunk/ btstack`
  1. cd into the btstack folder
> > `cd btstack`
  1. configure BTstack for iOS target
> > `./config-iphone.sh`
  1. build libBTstack and BTdaemon
> > `make`
  1. cd into the example/deamon folder
> > `cd example/daemon`
  1. in example/test.c, find the line with the hard-coded value for the MAC address of the WiiMote and enter yours. Mine has the address 00:19:1d:90:44:68
  1. build examples
> > `make`
  1. copy the l2cap-test to your iPhone. Replace 192.168.3.102 with the IP address of your device
> > `scp example/l2cap-test mobile@192.168.3.102:.`
  1. ssh into your device
> > `ssh mobile@192.168.3.102`
  1. sign the binaries on the device, if you did not install ldid on your build system
```
 ldid -S l2cap-test
```
  1. make sure Bluetooth is turned OFF in the Settings.app
  1. run the test
> > `./l2cap-test`
  1. check the output in both sessions. If everything works, the app will prompt you to make your WiiMote discoverable by pressing the buttons 1 and 2 together. Shortly after that you should get continuous accelerometer readings. You can press the Home button to quit the test app.

Important: My WLAN often breaks down when using Bluetooth. When logged in via SSH this looks like the app would not work or hang, when in reality the WLAN is just not working properly. Check the WLAN icon in the status bar. After the introduction of Internet tethering, I highly recommend to connect the iPhone via USB and use this connection for SSH. When using USB Tethering, my machine receives the IP address 192.168.20.3, and the iPhone can be accessed at 192.168.20.1.


# Details #

In main, the BTstack is opened and packet handlers are registered before the BTstack is asked to boot with the btstack\_set\_power\_mode command. All commands to control the BTstack are send asynchronously with the bt\_send\_cmd. Finally the run\_loop is executed. From there on, the rest of the test app runs as a finite state machine which processes events received from the BTstack. Be aware that error handling is barely performed. :)

Anyway, the different steps of the program are visible in the event handler. First, it reacts to the successful startup of the BTstack and set the local Bluetooth name. Then, pairing is enabled/disabled with the hci\_write\_authentication\_enable HCI command, which is caused by the command complete event of the hci\_hci\_write\_local\_name. Again, a command complete event will trigger the next action. Now, the BTstack is asked to open an L2CAP channel to the hard-coded WiiMote at PSM 0x13 (HID Interrupt) where reports from the HID device are received. Upon success, a second channel for PSM 0x11 (HID Control) is opened. This channel is necessary to enable the reporting of acceleration readings and send the command to set LEDs which also stops the LEDs from blinking. Finally, we're ready to receive HID status reports. See the HID and the WiiMote documentation for more details on this.


As this event handler shows, everything is event-triggered. After sending a command to the BTdaemon, which in turn sends it to the Bluetooth chipset, we wait for the corresponding event to continue with our application. Instead of writing this single even handler, it is much better to follow the concept of finite state machines. Based on our current state, an event such as HCI events, triggers the next action and the transition to another state. For more insight inton finite state machine, I highly recommend the book by Miro Samek.

# Develop BTstack apps in the iPhone Simulator #

To develop iPhone apps on the Mac, you need a serial Bluetooth module like the [Ericsson ROK Tester](http://www.tik.ee.ethz.ch/~beutel/projects/bttester/bt_tester.html) connected over a USB-to-Serial adapter, as the [HCI\_USB\_Transport](HCI_USB_Transport.md) does not work yet. With such a setup, you can configure BTstack for running on the Mac host, not the iPhone as described above. You also have to specify the UART device, see ./configure --help

For testing you run BTdaemon in one terminal before starting your app in the simulator. The app will then connect to the BTdaemon over the local UNIX domain socket.

# References #
  * [Human Interface Devices profile](http://www.bluetooth.com/NR/rdonlyres/0BE438ED-DC1B-41D1-AAC0-1AAA956097A2/980/HID_SPEC_V10.pdf)
  * [Great WiiMote documenation](http://wiibrew.org/wiki/Wiimote)
  * [Practical UML Statecharts by Miro Samek](http://www.amazon.com/Practical-UML-Statecharts-Second-Event-Driven/dp/0750687061/ref=sr_1_1?ie=UTF8&s=books&qid=1251484320&sr=8-1)


# Help #
If you really want to try the example app on your iPhone, but didn't get it to work although you've followed the instructions here, or, if you'd like to use Bluetooth in your own application (whatever OS/HW), please join the [BTstack Developer Forum](http://groups.google.com/group/btstack-dev).