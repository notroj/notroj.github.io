---
title: neon
tagline: HTTP/1.1 and WebDAV client library
logo: neon-logo.png
---

_neon_ is an HTTP/1.1 and WebDAV client library, with a C interface. Features:

* High-level wrappers for common HTTP and WebDAV operations (GET, MOVE, DELETE, etc)
Low-level interface to the HTTP request/response engine, allowing the use of arbitrary HTTP methods, headers, etc.
* Authentication support including Basic and Digest support, along with GSSAPI-based Negotiate on Unix, and SSPI-based Negotiate/NTLM on Win32
* SSL/TLS support using OpenSSL or GnuTLS; exposing an abstraction layer for verifying server certificates, handling client certificates, and examining certificate properties.
* Smartcard-based client certificates are also supported via a PKCS#11 wrapper interface
* Abstract interface to parsing XML using libxml2 or expat, and wrappers for simplifying handling XML HTTP response bodies
* WebDAV metadata support; wrappers for PROPFIND and PROPPATCH to simplify property manipulation

* * *

*   [Github repository](https://github.com/notroj/neon)
*   [Mailing list](http://lists.manyfish.co.uk/mailman/listinfo/neon)  
*   [List archive](http://lists.manyfish.co.uk/pipermail/neon/)
*   [neon-commits list](http://lists.manyfish.co.uk/mailman/listinfo/neon-commits)
*   Debian: [packages](http://packages.debian.org/search?keywords=neon)
*   Fedora: [package](https://apps.fedoraproject.org/packages/neon), [bugs](https://apps.fedoraproject.org/packages/neon/bugs/)
*   Gentoo: [package](http://packages.gentoo.org/package/net-misc/neon)
*   Solaris: [OpenCSW package](http://www.opencsw.org/packages/libneon27/)

neon is [free software](http://www.gnu.org/philosophy/free-sw.html), distributed under the [GNU Library GPL](http://www.gnu.org/copyleft/lgpl.html).

Patches, feature requests, bug reports, questions etc. can be [sent to](mailto:neon@lists.manyfish.co.uk) the neon [mailing list](http://lists.manyfish.co.uk/mailman/listinfo/neon/) (for which a [web archive](http://lists.manyfish.co.uk/pipermail/neon/) is also available). Alternatively, file pull requests or issues in the [neon github repository](https://github.com/notroj/neon). The [neon-commits list](http://lists.manyfish.co.uk/mailman/listinfo/neon-commits) receives commit messages from pushes to Github.

* * *

#### Changes in release 0.32.4 ([neon-0.32.4.tar.gz](neon-0.32.4.tar.gz)), 11th September 2022

* Fix Digest regression in allowing implicit algorithm= (issue #88)
* Fix Digest to safely allow spaces in usernames (without userhash)
* ne_ssl_trust_default_ca() now uses the system's trusted CAs
  with GnuTLS where supported (matching behaviour of OpenSSL)

#### Changes in release 0.32.3 ([neon-0.32.3.tar.gz](neon-0.32.3.tar.gz)), 4th September 2022

* Improvements and fixes to Windows build (Chun-wei Fan)
* Fix finding pkg-config when cross-compiling (Hugh McMaster)
* Fix Digest cnonce entropy sources in non-SSL builds
* Fix cases where Digest usernames were rejected as non-ASCII
* Fix build failures with OpenSSL 1.1 on some platforms

#### Changes in release 0.32.2 ([neon-0.32.2.tar.gz](neon-0.32.2.tar.gz)), 12th January 2022

* Fix auth handling for request-target of "*" (regressed since 0.31.x)
* Fix bindtextdomain() detection on OS X (Daniel Macks)
* Fix regeneration of docs in "make install" (Lonnie Abelbeck)
* Fixes for NetBSD build (Thomas Klausner)


#### Changes in release 0.32.1 ([neon-0.32.1.tar.gz](neon-0.32.1.tar.gz)), 20th September 2021

* Fix configure CFLAGS handling in Kerberos detection.
* Various spelling fixes.

#### Changes in release 0.32.0 ([neon-0.32.0.tar.gz](neon-0.32.0.tar.gz)), 20th September 2021

* Interface changes:
  * API and ABI backwards-compatible with 0.27.x and later
  * NE_AUTH_DIGEST now only enables RFC 2617/7616 auth by default;
   to enable weaker RFC 2069 Digest, use NE_AUTH_LEGACY_DIGEST
   (treated as a security enhancement, not an API/ABI break)
* Interface clarifications:
  * ne_auth.h: use of non-ASCII usernames with the ne_auth_creds
   callback type is now rejected for Digest auth since the
   encoding is not specified.  ne_add_auth() can be used instead.
  * ne_request.h: the ne_create_request_fn callback is passed the
   request-target using RFC 7230 terminology
* New interfaces and features:
  * ne_string.h: added ne_strhash(), ne_vstrhash(), ne_strparam()
  * ne_auth.h: added RFC 7616 (Digest authentication) support,
   including userhash=, username*= and SHA-2 algorithms
   (SHA-2 requires GnuTLS/OpenSSL).  added NE_AUTH_LEGACY_DIGEST
  * ne_auth.h: added ne_add_auth() unified auth callback interface,
   accepts (only) UTF-8 usernames, uses a larger password buffer,
   and has different/improved attempt counter semantics.
  * RFC 7617 scoping rules are now applied for Basic authentication.
  * ne_ssl.h: added ne_ssl_cert_hdigest()
  * ne_socket.h: added ne_sock_shutdown()
  * sendmsg()/send() are used with the MSG_NOSIGNAL flag to write to
   sockets on Unix, rather than write()/writev(), avoiding SIGPIPE
  * explicit_bzero() is used where available to clear credentials
* Bug fixes:
  * fixed TLS connection shutdown handling for OpenSSL 3
  * fix various Coverity and cppcheck warnings (Sebastian Reschke)
  * Kerberos library detection uses pkg-config where possible.
  * fix some configure checks on Win32 (Christopher Degawa)
  * fix some configure errors on MacOS (Ryan Schmidt)

#### Changes in release [neon 0.31.2](neon-0.31.2.tar.gz), 20th June 2020

* Fix ne_md5_read_ctx() with OpenSSL on big-endian architectures.
* Fix GCC 10 warning in PKCS#11 build.
* Fix OpenSSL build w/o deprecated APIs (Rosen Penev).
* Fix unnecessary MD5 test for non-Digest auth (Sebastian Reschke).
* Fix hang on SSL connection close with IIS (issue #11).
* Fix ar, ranlib detection when cross-compiling (Sergei Trofimovich).

#### Changes in release [neon 0.31.1](neon-0.31.1.tar.gz), 17th April 2020

* ADMIN: The neon website has moved to [https://notroj.github.io/neon/](https://notroj.github.io/neon/)
* Restore ne_md5_read_ctx() in OpenSSL build.
* Fix gcc warnings on Ubuntu (Jan-Marek Glogowski).
* Fix various spelling mistakes in docs and headers (thanks to FOSSIES).
* Fix ne_asctime_parse() (Eugenij-W).
* Fix build with LibreSSL (Juan RP).

#### Changes in release [neon 0.31.0](neon-0.31.0.tar.gz), 24th March 2020

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

* * *

[Joe Orton](mailto:joe@manyfish.co.uk)
