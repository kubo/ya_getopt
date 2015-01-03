ya_getopt - Yet another getopt
==============================

What is ya_getopt.
------------------

Ya_getopt is a drop-in replacement of [GNU C library getopt](http://man7.org/linux/man-pages/man3/getopt.3.html).
It has GNU getopt(), getopt_long() and getopt_long_only() except the following GNU extension.

> If *optstring* contains **W** followed by a semicolon, then **-W** **foo** is
> treated as the long option **--foo**.

The license is 2-clause BSD-style license. You can use the Linux getopt compatible function
under Windows, Solaris and so on without having to worry about license issue.

Note for contributors
---------------------

Don't send me a patch if you have looked at GNU C library getopt source code.
That's because I made this with clean room design to avoid the influence of the GNU GPL.

Please make a test script passed by the GNU C library getopt but not by ya_getopt instead.

License
-------

2-clause BSD-style license

Other getopt functions
----------------------

* [public domain AT&T getopt](https://www.google.co.jp/search?q=public+domain+at%26t+getopt)
* [Full getopt Port for Unicode and Multibyte Microsoft Visual C, C++, or MFC Projects](http://www.codeproject.com/Articles/157001/Full-getopt-Port-for-Unicode-and-Multibyte-Microso)
