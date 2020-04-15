---
title: neon
logo: neon-logo.png
---

_neon_ is an HTTP and WebDAV client library, with a C interface. Features:

*   High-level wrappers for common HTTP and WebDAV operations (GET, MOVE, DELETE, etc)
Low-level interface to the HTTP request/response engine, allowing the use of arbitrary HTTP methods, headers, etc.*   Authentication support including Basic and Digest support, along with GSSAPI-based Negotiate on Unix, and SSPI-based Negotiate/NTLM on Win32
*   SSL/TLS support using OpenSSL or GnuTLS; exposing an abstraction layer for verifying server certificates, handling client certificates, and examining certificate properties.
* Smartcard-based client certificates are also supported via a PKCS#11 wrapper interface
* Abstract interface to parsing XML using libxml2 or expat, and wrappers for simplifying handling XML HTTP response bodies
* WebDAV metadata support; wrappers for PROPFIND and PROPPATCH to simplify property manipulation

* * *

*   [Mailing list](http://lists.manyfish.co.uk/mailman/listinfo/neon)  
*   [List archive](http://lists.manyfish.co.uk/pipermail/neon/)
*   [neon-commits list](http://lists.manyfish.co.uk/mailman/listinfo/neon-commits)
*   Debian: [packages](http://packages.debian.org/search?keywords=neon)
*   Fedora: [package](https://admin.fedoraproject.org/pkgdb/packages/name/neon), [bugs](https://admin.fedoraproject.org/pkgdb/packages/bugs/neon)
*   Gentoo: [package](http://packages.gentoo.org/package/net-misc/neon)
*   Solaris: [OpenCSW package](http://www.opencsw.org/packages/libneon27/)

neon is [free software](http://www.gnu.org/philosophy/free-sw.html), distributed under the [GNU Library GPL](http://www.gnu.org/copyleft/lgpl.html).

Patches, feature requests, bug reports, questions etc. can be [sent to](mailto:neon@lists.manyfish.co.uk) the neon [mailing list](http://lists.manyfish.co.uk/mailman/listinfo/neon/) (for which a [web archive](http://lists.manyfish.co.uk/pipermail/neon/) is also available). Alternatively, file pull requests or issues in the [neon github repository](https://github.com/notroj/neon). The [neon-commits list](http://lists.manyfish.co.uk/mailman/listinfo/neon-commits) receives commit messages from pushes to Github.

* * *

### Current Release

**Please note:** The neon API and ABI are stable and maintain backwards compatibility from 0.27.x through 0.31.x.

*   Source code: **[neon-0.31.0.tar.gz](http://www.webdav.org/neon/neon-0.31.0.tar.gz)**
*   [Github repository](https://github.com/notroj/neon)

* * *

#### Changes in release [neon 0.31.0](http://www.webdav.org/neon/neon-0.31.0.tar.gz), 24th March 2020

*   Interface changes:
    *   none, API and ABI backwards-compatible with 0.27.x and later
*   New interfaces and features:
    *   add more gcc "nonnull" attributes to ne\_request\_\* functions.
    *   for OpenSSL builds, ne\_md5 code uses the OpenSSL implementation
    *   add NE\_SESSFLAG\_SHAREPOINT session flag which enables workarounds< for RFC non-compliance issues in Sharepoint (thanks to Jan-Marek Glogowski and Giuseppe Castagno)
    *   ne\_uri.h: add ne\_path\_escapef() in support of above
    *   ne\_207.h: add ne\_207\_set\_flags() likewise in support of above
*   API clarification:
    *   ne\_version\_match() behaviour now matches actual 0.27+ ABI history
*   Bug fixes:
    *   fixes for OpenSSL 1.1.1 and TLSv1.3 support
    *   fix crash with GnuTLS in client cert support (Henrik Holst)
    *   fix possible crash in ne\_set\_request\_flag()
    *   fix build with libxml2 2.9.10 and later
    *   fix handling lock timeouts >LONG\_MAX (Giuseppe Castagno)

#### Changes in release [neon 0.30.2](http://www.webdav.org/neon/neon-0.30.2.tar.gz), 30th September 2016 ([PGP signature](http://www.webdav.org/neon/neon-0.30.2.tar.gz.asc))

*   Add support for OpenSSL 1.1.x (Kurt Roeckx).
*   Fix PKCS#11 support under GnuTLS 3.x.
    *   PKCS#11 API no longer supported with GnuTLS 2.x

* * *

[Joe Orton](mailto:joe@manyfish.co.uk)
