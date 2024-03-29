ControlX10::CM17
VERSION=0.06, 11 October 1999

Hello home automators:

The FireCracker (CM17A) is a send-only X10 controller that connects
to a serial port and transmits commands via RF to X10 transceivers.
This module translates human-readable commands (eg. 'A2J') into the
bit patterns and control signal pulses accepted by the CM17.

You will need one of the SerialPort modules from CPAN to generate the
actual hardware commands to the port. If you are running Windows 95 or
later, you want the Win32::SerialPort module. The linux equivalent is
the Device::SerialPort module. Device::SerialPort will also run on
other POSIX Operating Systems - but the CM17 module uses ioctl calls
that may not be supported on all of the (yet).

This is a cross-platform module. All of the files except README.txt
are LF-only terminations. You will need a better editor than Notepad
to read them on Win32. README.txt is README with CRLF.

FILES:

    Changes		- for history lovers
    Makefile.PL		- the "starting point" for traditional reasons
    MANIFEST		- file list
    README		- this file for CPAN
    README.txt		- this file for DOS
    CM17.pm		- the reason you're reading this

    t/test1.t		- RUN ME FIRST, basic tests
    eg/eg_cm17.plx	- simple On/Off/Dim_Lamp demo

OPERATION:

The FireCracker derives its power supply from either the RTS or
DTR signals from the serial port. At least one of these signals
must be high at all times to ensure that power is not lost from
the FireCracker. The signals are pulsed to transmit a bit (DTR
for '1' and RTS for '0'). The normal rx/tx read/write lines are
not used by the device - but are passed through to allow another
serial device to be connected (as long as it does not require
hardware handshaking). The $serial_port object that is needed by
the CM17 module fully supports the pass-through feature.

INSTALL and TEST:

You will need suitable permissions to open the port. If the port is also
used for logins, you will need to create a lockfile (/var/lock/LCK..ttyS0
on my Redhat 5.2 system). Just touch it, the contents are not important.
They may be someday. But not yet. You might need to be "root" for that.

On linux and Unix, this distribution uses Makefile.PL and the "standard"
install sequence for CPAN modules:
	perl Makefile.PL
	make
	make test
	make install

On Win32, Makefile.PL creates equivalent scripts for the "make-deprived"
and follows a similar sequence.
	perl Makefile.PL
	perl test.pl
	perl install.pl

Both sequences create install files and directories. The test emulates
a CM17 - it is not necessary to select a port or connect the hardware.

The "eg_cm17.plx" demo is a cross-platform version of a demo previously
posted and included with MisterHouse. It expects an X10 appliance switch
at address A1 and a lamp at address A2. It uses the port defaults "COM1"
on Win32 and "/dev/ttyS0" on linux. You can either edit the port choice
or specify it with 'perl eg_cm17.plx PORT'.

Watch for updates at:

%%%% http://members.aol.com/Bbirthisel/alpha.html
%%%% http://misterhouse.net
or CPAN under authors/id/B/BB/BBIRTH or ControlX10::CM17

CPAN packaging and module documentation by Bill Birthisel.

Copyright (C) 1999, Bruce Winter. All rights reserved. This module is
free software; you can redistribute it and/or modify it under the same
terms as Perl itself.
