Welcome to softflowd, a flow-based network monitor.

Introduction
------------

softflowd listens promiscuously on a network interface and semi-statefully
tracks network flows. These flows can be reported using NetFlow version 1, 5 
or 9 datagrams. softflowd is fully IPv6 capable: it can track IPv6 flows and 
export to IPv6 hosts.

More details about softflowd's function and usage may be found in the
supplied manpages, which you can view prior to installation using

/usr/bin/nroff -c -mandoc softflowd.8 | less
/usr/bin/nroff -c -mandoc softflowctl.8 | less

If you are in need of a NetFlow collector, you may be interested in 
softflowd's companion project "flowd" (http://www.mindrot.org/flowd.html). 
flowd is a NetFlow collector that is maintained in parallel with
softflowd and includes a few handy features, such as the ability
to filter flows it receives as well as Perl and Python APIs to its
storage format. NB. You don't have to use flowd: any NetFlow compatible 
collector should work with softflowd. An example Perl collector is included 
for testing purposes as collector.pl, but it doesn't yet support NetFlow v.9

Installing
----------

Building softflowd should be as simple as typing:

./configure
make
make install

Unfortunately some systems like to make life complicated. Things work
fine on the systems that I develop and test on (OpenBSD and Linux).
There is peliminary support for Solaris 9 (i.e. it compiled), but no
testing on this platform has been performed.

Licensing
---------

Softflowd is licensed under a two-term BSD license (see the source
files for details). The code in sys-tree.h is Copyright Niels Provos
<provos@citi.umich.edu> and comes straight from OpenBSD CVS, convtime.c
comes is Copyright Kevin Steves and comes from OpenSSH (misc.c). Both
of these files are licensed under two-term BSD licenses too. strlcpy.c,
strlcat.c and closefrom.c also come from OpenBSD CVS and are Copyright
Todd C. Miller. Please refer to the LICENSE file for full details.

Reporting Bugs
--------------

Please report bugs in softflowd to http://bugzilla.mindrot.org/ If you
find a security bug, please report it directly by email. If you have any
feedback or questions, please email me:

Contributing
------------

Softflowd has an extensive TODO list of interesting features, large and
small, that are waiting to be implemented. If you are interested in
helping, please contact me.

The latest source code may (*no longer*) be obtained from Google Code:
https://code.google.com/archive/p/softflowd/

Damien Miller <djm@mindrot.org>

Google Code Project Description
-------------------------------

## A software NetFlow probe

Softflowd is flow-based network traffic analyser capable of Cisco NetFlow data export. Softflowd semi-statefully tracks traffic flows recorded by listening on a network interface or by reading a packet capture file. These flows may be reported via NetFlow to a collecting host or summarised within softflowd itself.

Softflowd supports Netflow versions 1, 5 and 9 and is fully IPv6-capable - it can track IPv6 flows and send export datagrams via IPv6. It also supports export to multicast groups, allowing for redundant flow collectors.

## Details

Softflowd semi-statefully tracks traffic flows. Upon expiry of a flow, its statistics are accumulated and reports them to a designated collector host using the standard NetFlow protocol. Currently the statistics collected are summaries only: min/max/avg/total bytes, packets on a aggregate or per-protocol basis.

Softflowd can export using NetFlow version 1, 5 or 9 datagrams and it is fully IPv6 capable: it can track and report on IPv6 traffic and flow export datagrams can be sent to an IPv6 host. Any standard NetFlow collector should be able to process the reports from softflowd.

As softflowd watches traffic promiscuously, it is likely to place additional load on hosts or gateways on which it is installed. However, this implementation has been designed to minimise this load as much as possible. Alternately, softflowd can read pcap save files recorded from tcpdump and friends.

Unless reading from a traffic dump, softflowd run as a daemon. A "remote control" program (softflowctl) is included which allows runtime control and extraction of statistics from a daemonised softflowd.

Softflowd is developed on Linux and OpenBSD. It requires libpcap and its associated headers to build, these are available from tcpdump.org, or from your operating system vendor. As of version 0.9, there is some support for Solaris but this is still experimental.

