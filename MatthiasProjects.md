# Introduction #
Thanks for all the interesting project proposals from all of you. I'm working full time in a start-up company and BTstack is "just" my main hobby project

# Tasks/Projects #
  * BTstack GPS:
    * create BTstackGPSd
    * add option to enforce pairing
    * Server option: provide iPhone or iPad 3G GPS data to BTstack GPS
  * hid-support:
    * Add mouse pointer simulation. send touch event for mouse pointer point
    * add hi-res mouse pointer for iPhone 4 Retina display
    * require heartbeat from apps (Veency, BTstack Mouse, SynergyClient) to turn off when app/extension crashes
  * BTstack Keyboard 1.1 update, lots of details to take care of like
    * split into background daemon + config app/preference bundle
    * auto-accept incoming connections
    * use new 3.2+ events for cursors, volume, brightness
    * accented chars
    * disable auto-correction
    * more layouts
    * layout switcher
    * alternate selection for Asian language
    * support Freedom Universal SPP keyboard
    * use new RFCOMM API
  * Improve use of remote desktop apps on iPad
  * Implement GameKit for Mac and other non-iOS devices
  * Other private/consulting projects

# Other Projects... #
... I don't seem to tackle soon, feel free to contact me if you work on them :)
  * Add support for the Wii Balance board:
    * enable data reporting according to [wiibrew.org documentation](http://wiibrew.org/wiki/Wiimote/Extension_Controllers#Balance_Board)
    * create 3D model of the balance board for OpenGL display
  * Audio stuff A2DP, HFP...
  * Other Bluetooth profiles
  * [iOS client for Synergy protocol](http://www.tuaw.com/2010/06/28/found-footage-synergy-on-ios/) - not Bluetooth related, but a nice little project.
    * ~~iSynergyClient 0.8~~ submitted to BigBoss repo 4th of July
    * released as open source project at http://code.google.com/p/isynergyclient/

# Completed #
  * ~~Blutrol: Play games with iCade (later: Wiimote, Zeemote, PS3 SixAxis, and iControlPad..)~~
  * ~~BTstack port for EmbeddedSystems~~
  * ~~Celeste Version 1.0~~
  * ~~Full RFCOMM support: implemented, released May 1, 2010~~
  * ~~Full OBEX support for iOS~~
    * [Bluetooth file sharing for iOS, at last.](http://getceleste.com) released
  * ~~iPhone as Keyboard & Touchpad for other devices like PC, PS3, ...~~ released March 23, 2011 [WeBe++](http://www.weblooks.ch/webe-plus/) Dec 10th, 2010
  * ~~Handle multiple L2CAP commands in a single signaling packet~~ [revision 658](https://code.google.com/p/btstack/source/detail?r=658)
  * ~~BTstack on iPhone OS 4.0~~
    * ~~Is working but not released yet.~~ Release [revision 757](https://code.google.com/p/btstack/source/detail?r=757) June 22n
    * ~~Caveat: there is no BTstack icon in the status bar~~ Solved by [libstatusbar](http://apt.thebigboss.org/onepackage.php?bundleid=libstatusbar&db=) July 4rd
  * L2CAP Credit-based Flowcontrol
    * ~~query BT module for nr and size of ACL packets (HCI read buffer size command)~~ [r818](https://code.google.com/p/btstack/source/detail?r=818)
    * ~~keep track of free ACL buffers in BT module (Number Of Completed Packets Event)~~ [r820](https://code.google.com/p/btstack/source/detail?r=820)
    * ~~implement mechanism to _park_ socket connections~~
      * ~~add linked\_list\_add\_tail(list, item)~~
      * ~~assert socket callback handlers return 0~~
      * ~~add list of parked connections~~
      * ~~if dispatch fails: remove from run loop and add to parked list~~
    * ~~have send\_l2cap and send\_acl return error -1 if no space on BT module~~
    * ~~implement "call re-dispatch on all parked connections, in FIFO order"~~
      * ~~if re-dispatch succeeds: remove from parked list and add to run loop~~
    * ~~provide credit-based flow control ("probably ready for x data packets")~~
      * ~~on number completed packets:~~
        * ~~call re-dispatch on parked connections~~
        * ~~hand out credits if conditions are met~~
    * ~~write L2CAP performance test apps for both client and server mode for Apple's Bluetooth Explorer using PSM 0xdead~~
    * ~~test on device~~
      * ~~[r848](https://code.google.com/p/btstack/source/detail?r=848) 40 KB/s incoming,  1 KB/s outgoing :(~~
      * ~~[r849](https://code.google.com/p/btstack/source/detail?r=849) 40 KB/s incoming, 45 KB/s outgoing :)~~
  * L2CAP
    * ~~keep track of remote incoming MTU~~ [r750](https://code.google.com/p/btstack/source/detail?r=750)
    * ~~use 1021 byte L2CAP buffer (3-DH5) in BTdaemon~~
    * ~~limit L2CAP MTU by Bluetooth controller ACL packet buffers~~
  * ~~[Service Discovery Protocol](SDP.md)~~
    * ~~limit amount of information in responses to remote L2CAP MTU~~ [revision 753](https://code.google.com/p/btstack/source/detail?r=753)
    * ~~Figure out a way to serve records larger than 255 bytes~~ ~ 1000 byte packets should be enough for most services
  * ~~HCI - iOS Remote Device DB~~
    * ~~handle link key management in BTdaemon~~
    * ~~store new link keys in plist on file system~~
    * ~~answer link key requests by Bluetooth module~~
    * ~~store remote names in plist~~
    * ~~send BTSTACK\_EVENT\_REMOTE\_NAME\_CHACHED for each device in a inquiry result~~
  * ~~BTstack GPS 1.6: ~
    *~~ use new RFCOMM API ~
    * ~~provide information if BTstack GPS is active ~
    *~~ add option to throttle update rate ~
    * ~~use speed from NMEA messages ~
    *~~ use course from NMEA messages ~
    * ~~use accuracy from NMEA messages~~