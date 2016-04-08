# Introduction #

Most people that contacted me have expressed interest in the use of RFCOMM. The RFCOMM protocol provides emulation of serial ports over the L2CAP protocol. The protocol is based on the ETSI standard TS 07.10, a standard in the Telecom industry.

RFCOMM is commonly used:
  * for Bluetooth GPS Receivers.
  * to provide Bluetooth to legacy devices which used RS232 before. E.g., laser BarCode scanners, early mobile/foldable Bluetooth keyboards, wireless interface for hobby embedded system and robotic projects.
  * as a basis for other legacy protocols like OBEX and PPP.

# Why RFCOMM is not a good idea for new projects #
Most communication devices work on a packet basis, i.e., they communicate by passing messages back and forth. A GPS receiver periodically sends position packets, a BarCode scanner will send individual BarCode IDs, ...

For these use cases, RFCOMM is a rather cumbersome protocol given that all communication in Bluetooth is inherently packet based. The lower layer L2CAP already provides a perfect abstraction for sending packets between parties. Now, RFCOMM emulates a serial cable where bytes can be sent individually. For the previously mentioned applications, this means that the application unnecessarily has to detect packet frames again, although the underlying communication already is packet-based.

That said, you cannot change the gadget you own, so we need RFCOMM support in BTstack... :)

Another argument for the use of RFCOMM could be made based on the RFCOMM support that exists in all major operating systems. A virtual serial connection can be configure via the OS and an application can communicate with a Bluetooth device without even knowing that this device uses Bluetooth. The benefit of this approach is also its main drawback. All configuration has to be manually conducted by the user via the OS preferences (or command-line). An application cannot even scan for devices by itself. Using RFCOMM via a proper Bluetooth API provides this flexibility but also renders this benefit of seamless integration worthless.

# Details #
RFCOMM is implemented as part of BTstack since May 1st, 2011. [more info](http://groups.google.com/group/btstack-dev/browse_thread/thread/8f2a1635ecfeaf8f)

# Specs #
  * [TS 07.10 aka TS 101 369](https://www.fer.hr/_download/repository/ts_101369v060300p.pdf) on which is RFOMM is based.
  * [rfcom.pdf](http://bluetooth.com/English/Technology/Building/Pages/Specification.aspx) describes the adaption of TS 07.10 for RFCOMM, these are both clarification and/or details.
  * [SPP\_SPEC\_V11.pdf](http://bluetooth.com/English/Technology/Building/Pages/Specification.aspx) specifies how RFCOMM is used as main part of the Serial Port Profile.

# Tutorial #
[Chapter 10](http://authors.phptr.com/bluetooth/bray/pdf/cr_ch10.pdf) of [Bluetooth without Cables](http://authors.phptr.com/bluetooth/bray/index.html) from Prentice Hall.

# Example Logs #
[Apple PacketLogger log connecting to a ZeeMote JS1](http://btstack.googlecode.com/svn/files/ZeemoteRFCOMM.pklg)

# RFCOMM Initialization #
The interesting RFCOMM messages from the log above:

![http://btstack.googlecode.com/svn/files/RFCOMM-Initialization.png](http://btstack.googlecode.com/svn/files/RFCOMM-Initialization.png)