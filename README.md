# surreptitious

A surreptitious/stealthy port scanner

History - I wrote this circa 2015 based on an incident at an intelligence agency.
My goal was to show them that a little bit of wisely crafted python could thwart
some of their multi-million dollar expenditures. Their arrogance certainly was
a major inspiration for me to write this. And for the record they were never able
to detect or stop this code :-)

This was written on Linux and has been used/tested on Fedora and Debian/Ubuntu.
I have no plans or time to port/test to/on any different platforms. If you wanna
contribute in this way or any other way let me know:

    andres [at] neurofuzzsecurity dot com

This prog is intended to be used for legal purposes.

This prog is not meant to be run on a LAN as it uses tor sockets to route each
port check via a different internet based path. So the goal is to scan a public
facing entity (server, etc) in a stealthy manner that cannot be detected.


Requirements:

- python (2.x family currently)
- tor
- proxychains4
- nmap
- neurofuzz_toolkit (gets downloaded and set up by get_nf_toolkit.py)


Getting Started:

    - git clone git@github.com:neuroFuzz/surreptitious.git
    - cd surreptitious
    - python get_nf_toolkit.py


Usage:

    python surreptitious.py -t ip_address -s 1 -e 65535 -p nmap_results

    -t = target ip address to be scanned
    -s = start port
    -e = end port
    -p = path/directory where the final nmap results files will be saved


Notes:

    - currently only scans for TCP ports

    - this prog works in 2 waves:

        - wave 1 is the long, slow and stealthy port scan doing nothing fancy,
            pure check to see if a port is open and if something is listening
            on the other end
        - wave 2 - we take the results from wave 1 and pass those in to nmap
            so that the nmap scan is focused exclusively on ports we know/think
            are open. here we do fancy stuff like service and OS detection via
            nmap's features. OS detection via nmap requires root privilege

    - this IS NOT fast, that is by design - it is written to try to NEVER trip
        a sensor or alert a sentry

    - Writes out the nmap results to the dir set forth with -p, file names are
        in the following format:

            timestamp_ipaddress

        if you dont know how to convert unix timestamps to something that makes
        sense to you ..... you shouldn't be running a prog like this one :-)

TODO:

    - WTF do I do about UDP ports ???
    - Improve final output
