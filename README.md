ya_getopt - Yet another getopt compatible with GNU C library getopt
===================================================================

What is ya_getopt.
------------------

Ya_getopt is compatible with GNU C library getopt used on Linux and is licensed under 2-clause BSD-style license.
This means that you can use the Linux getopt compatible function under Windows, Solaris and so on
without having to worry about license issue.

Note for contributors
---------------------

Don't send me a patch if you have looked at GNU C library getopt source code.
That's because I made this with clean room design to avoid the influence of the GNU GPL.

Please make a test script passed by the GNU C glibrary getopt but not by ya_getopt instead.

License
-------

2-clause BSD-style license
