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
* WebDAV support; including locking, property manipulation and retrieval, ACL support

* * *

*   [Github repository](https://github.com/notroj/neon)
*   [Documentation](/neon-docs/)
*   [Discussion forum](https://github.com/notroj/neon/discussions)
*   [Bug reports](https://github.com/notroj/neon/issues)
*   Debian: [packages](http://packages.debian.org/search?keywords=neon)
*   Fedora: [package](https://src.fedoraproject.org/rpms/libneon27)
*   Gentoo: [package](http://packages.gentoo.org/package/net-libs/neon)
*   Solaris: [OpenCSW package](http://www.opencsw.org/packages/libneon27/)

neon is [free software](http://www.gnu.org/philosophy/free-sw.html), distributed under the [GNU Library GPL](http://www.gnu.org/copyleft/lgpl.html).

Feature requests, bug reports etc should be reported via the [Github repository](https://github.com/notroj/neon).

* * *

#### Changes in release 0.35.0 ([neon-0.35.0.tar.gz](neon-0.35.0.tar.gz)), 15th July 2025

* Interface changes:
  * API and ABI backwards-compatible with 0.27.x and later
  * pakchois-based PKCS#11 support is now deprecated
* Interface clarifications:
  * ne_md5_read_ctx() may return NULL
* New interfaces and features:
  * ne_request.h: add ne_get_response_retry_after()
  * ne_uri.h: add NE_PATH_NONPC escaping rule
  * ne_string.h: add ne_strhextoul()
  * ne_ssl.h: add ne_ssl_clicert_fromuri(), a simpler API
   to retrieve client certs based on (e.g.) PKCS#11 URIs;
   only supported with OpenSSL currently.
  * ne_session.h: add ne_status_handshake to notifier API
* Bug fixes:
  * ne_path_escape() now follows NE_PATH_NONPC pct-encoding
   rule by default (fixes #181)
  * ne_md5_*(): for OpenSSL, now uses the EVP* API
  * session caching fixes for OpenSSL
* "BUGS" document removed, use https://github.com/notroj/neon/issues


#### Changes in release 0.34.2 ([neon-0.34.2.tar.gz](neon-0.34.2.tar.gz)), 15th April 2025

* Fix regression in NTLM auth in 0.34.0 (issue #190).
* Add docs for ne_ssl_proto_name, ne_ssl_protovers, ne_get_request_target.

#### Changes in release 0.34.1 ([neon-0.34.1.tar.gz](neon-0.34.1.tar.gz)), 14th April 2025

* Fix regression in 207 parsing of <status> elements which omit
  a reason-phrase (issue #188).
* Fix ne_move() to submit lock tokens for the parent collection
  of a source resource locked with depth: 0.

#### Changes in release 0.34.0 ([neon-0.34.0.tar.gz](neon-0.34.0.tar.gz)), 23rd November 2024

* Interface changes:
  * API and ABI backwards-compatible with 0.27.x and later
  * NE_SESSFLAG_SSLv2 is now ignored
* New interfaces and features:
  * ne_request.h: add ne_get_response_location(),
   add ne_get_request_target()
  * ne_redirect.h: adds relative URI resolution per RFC 9110
  * ne_socket.h: add ne_iaddr_set_scope(), ne_iaddr_get_scope(),
   ne_sock_getproto()
  * ne_session.h: add NE_SESSFLAG_STRICT session flag
  * ne_session.h: ne_session_create() now accepts scoped IPv6
   link-local literal addresses following the RFC 6874 syntax;
  * ne_session.h: add ne_ssl_set_protovers() to configure TLS
   protocol version ranges
  * ne_utils.h: add NE_FEATURE_GSSAPI, NE_FEATURE_LIBPXY feature flags
  * ne_ssl.h: add ne_ssl_proto_name()
  * HTTP strictness/compliance updated for RFC 9110/9112;
   notably stricter in parsing header field line, chunked
   transfer-coding, status-line.
* Bug fixes:
  * auth: the 'realm' string passed to credentials callback is now
   cleaned of non-printable characters.
* Documentation & header updates for RFC 9110/9112.
* New NE_MINIMUM_VERSION() autoconf macro for better version handling.

#### Changes in release 0.33.0 ([neon-0.33.0.tar.gz](neon-0.33.0.tar.gz)), 29th January 2024

* Interface changes:
 * API and ABI backwards-compatible with 0.27.x and later
* Interface clarifications:
   * ne_locks.h: note that returned lock may have a different URI
     than the path passed to ne_lock_discover() due to added
     support for RFC 4918 "lockroot" in lock discovery
   * ne_request.h: ne_request_create() takes a "target" rather
     than a path and this can also be an absolute-URI
   * ne_request.h: never-used ne_free_hooks typedef removed
   * ne_dates.h: clarified error cases (behaviour unchanged)
   * ne_session.h: ne_session_create() 'host' must match RFC 3986
     syntax; IPv6 literal addresses must use [] brackets
* New interfaces and features:
   * added new configure flag --enable-auto-libproxy which enables
     libproxy by default for new sessions (Jan-Michael Brummer)
   * ne_locks.h: added DAV:lockroot support per RFC 4918
   * ne_ssl.h: ne_ssl_trust_default_ca() now a no-op for non-SSL sessions
    * ne_request.h: add ne_add_interim_handler() to handle interim
   (1xx) responses; headers in interim responses are now accessible
   * ne_basic.h: add ne_putbuf()
   * ne_strhash: SHA-512/256 now supported for LibreSSL 3.8+ (orbea)
   * response handling no longer applies a maximum limit on 1xx interim
   responses; an overall timeout equal to the read timeout is now
   applied if a read timeout is configured and 1XXTIMEOUT is enabled
   * ne_request.h: add NE_REQFLAG_1XXTIMEOUT
* Bug fixes:
  * test suite now works correctly on IPv6-only hosts (Jeremy Sowden)
  * fixes for building against LibreSSL (orbea)
  * ne_uri_parse() fixes for handling URI with no path and catch
   some invalid URIs which were allowed (fasticc)
  * retry requests after a 408 response on a persisted connection
  * 207 error strings are cleaned and compressed to a single line
  * fixed thread-safety in ne_rfc1123_date where gmtime_r is available
  * ne_lock_refresh() fixed to use a non-idempotent request
  * TLS name verification updated to match RFC 9110/6125, added strict
   handling of IP literals vs DNS names

#### Changes in release 0.32.5 ([neon-0.32.5.tar.gz](neon-0.32.5.tar.gz)), 21st January 2023

* NOTE: Since 0.32.0 the "$KRB5_CONFIG" environment variable is ignored
  when running configure. Use KRB5_CONF_TOOL instead to specify an
  alternative to /usr/bin/krb5-config.
* Fail for configure --with-gssapi if GSSAPI can't be enabled (issue #102)
* Add Georgian translation (NorwayFun)
* Fixes for Windows MSYS2/MinGW build, including cross-build (Jim Klimov)

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
