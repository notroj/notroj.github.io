---
title: litmus
logo: shot.png
---

_litmus_ is a [WebDAV](https://tools.ietf.org/html/rfc4918) server test suite, which aims to test whether a server is compliant with the WebDAV protocol as specified in RFC2518; current tests cover:

*   OPTIONS for DAV: header
*   PUT, GET with byte comparison
*   MKCOL
*   DELETE (collections, non-collections)
*   COPY, MOVE using combinations of:
    *   overwrite t/f
    *   destination exists/doesn't exist
    *   collection/non-collection
*   Property manipulation and querying:
    *   set, delete, replace properties
    *   persist dead props across COPY
    *   namespace handling
*   Locking
    *   attempts to modify locked resource (as lock owner, not owner)
    *   shared/exclusive locks
    *   lock discovery
    *   collection locking
    *   lock refresh

Note that a server which passes all these tests will not necessarily work with any real DAV clients; though the chances are good. _litmus_ is built using the [neon](https://notroj.github.io/neon/) library, so supports digest and basic authentication, TLS/SSL, and proxy servers.

* * *

*   [Github repository](https://github.com/notroj/litmus)
*   [Discussion forum](https://github.com/notroj/litmus/discussions)
*   [Bug reports](https://github.com/notroj/litmus/issues)

_litmus_ has been tested on Linux, Solaris, FreeBSD, CygWin, and many other Unix systems. 

* * *

#### Changes in release [litmus 0.16](litmus-0.16.tar.gz), 23 November 2024

* New tests:
  * props: test that deleting a property twice succeeds
* Bug fixes:
  * basic: fix path used in put_location test (Martin Vobruba)
* Various error/warning references updated from RFC 2518 to 4918
* Update to neon 0.34.0.

#### Changes in release [litmus 0.15](litmus-0.15.tar.gz), 25 February 2024

* New tests:
  * props: test for DAV:getlastmodified property value
  * basic: test Location header if returned by PUT
* Bug fixes:
  * fix crash on invalid URL command-line (Glenn Strauss)
  * locks: fixed lockscope check error reporting (Glenn Strauss)
  * send correct request content-type in all PROPFIND/PROPPATCH tests
  * various error/warning references updated from RFC 2518 to 4918
* Updated to neon 0.33.0.

#### Changes in release [litmus 0.14](litmus-0.14.tar.gz), 29 January 2022

* Changed tests:
  * copymove: copy_shallow fixed to check for shallow copy correctly (Javier Godoy)
  * basic: fix test for PUT giving 409 with no parent collection
   **NOTE**: this test now fails with Apache httpd < 2.4.55
* Update to neon 0.32.4.

#### Changes in release [litmus 0.13](litmus-0.13.tar.gz), 9 December 2011 ([PGP signature](litmus-0.13.tar.gz.asc))

*   Changed tests:
    *   locks: owner\_modify checks that PROPPATCH works against a locked resource (thanks to Javier Godoy)
*   Support PKCS#12 client cert with --client-cert/-c (Alejandro Alvarez Ayllon)
*   Update to neon 0.29.6.

#### Changes in release [litmus 0.12.1](litmus-0.12.1.tar.gz), 6 November 2008 ([PGP signature](litmus-0.12.1.tar.gz.asc))

*   Changed tests:
    *   locks: remove DELETE from unmapped URI LOCK/DELETE/UNLOCK sequence
    *   locks: fail if LOCK gives a lockscope which does not match that requested
    *   props: use real URIs for the property namespaces

#### Changes in release [litmus 0.12](litmus-0.12.tar.gz), 29 September 2008 ([PGP signature](litmus-0.12.tar.gz.asc))

*   New tests:
    *   props: unmapped\_lock (Henrik Holst)
    *   basic: put\_no\_parent
*   Changed tests:
    *   props: propvalnspace - use a valid URI in the 'foo' element
*   Update to neon 0.28.3; support neon 0.25.x->0.28.x

#### Changes in release [litmus 0.11](litmus-0.11.tar.gz), 23 January 2007 ([PGP signature](litmus-0.11.tar.gz.asc))

*   New tests from Julian Reschke:
    *   props: test for correct PROPPATCH propertyupdate evaluation order
    *   copymove: test for "Depth: 0" COPY of collection
*   Test URL is no longer path-escaped internally.
*   Update to neon 0.26.3.

#### Changes in release [litmus 0.10.5](litmus-0.10.5.tar.gz), 2 November 2005 ([PGP signature](litmus-0.10.5.tar.gz.asc))

*   Add another test for handling of unknown state tokens in an If: header.
*   Update to neon 0.25.4.

#### Changes in release [litmus 0.10.4](litmus-0.10.4.tar.gz), 17 September 2005 ([PGP signature](litmus-0.10.4.tar.gz.asc))

*   Fix possible crashes in lock discovery.
*   Update to neon 0.25.3.

#### Changes in release [litmus 0.10.3](litmus-0.10.3.tar.gz), 17 August 2005 ([PGP signature](litmus-0.10.3.tar.gz.asc))

*   Fix VPATH builds (Mike Castle).
*   Fix build with bundled expat.
*   Update to neon 0.25.2.

#### Changes in release [litmus 0.10.2](litmus-0.10.2.tar.gz), 29 March 2005 ([PGP signature](litmus-0.10.2.tar.gz.asc))

*   Fix build on Mac OS X.
*   Fixes for the "largefile" test suite.

#### Changes in release [litmus 0.10.1](litmus-0.10.1.tar.gz), 12 September 2004 ([PGP signature](litmus-0.10.1.tar.gz.asc))

*   Add check for DELETE safety with #fragment in Request-URI.

#### Changes in release [litmus 0.10.0](litmus-0.10.0.tar.gz), 12 September 2004 ([PGP signature](litmus-0.10.tar.gz.asc))

*   Add some basic collection locking tests.
*   Correct fail\_complex\_cond\_put to really send an invalid etag as intended, thanks to Tod Sambar.
*   Describe the conditional PUT tests in the FAQ.
*   Add test for PROPFIND extensibility rules in request body.
*   Skip the 'expect100' in the 'http' suite for an SSL session.

#### Changes in release [litmus 0.9.4](litmus-0.9.4.tar.gz), 24 August 2003 ([PGP signature](litmus-0.9.4.tar.gz.asc))

*   Correct fix for comparison of absolute URIs in PROPFIND responses, thanks to Thomas Kemmer.

#### Changes in release [litmus 0.9.3](litmus-0.9.3.tar.gz), 19 August 2003 ([PGP signature](litmus-0.9.3.tar.gz.asc))

*   Fix some segfaults when some lock tests fail (thanks to Thomas Kemmer).
*   Fix comparison of hrefs in PROPFIND responses containing absolute https URI.
*   Run conditional PUT tests against exclusive-locked resource.

#### Changes in release [litmus 0.9.2](litmus-0.9.2.tar.gz), 20 March 2003 ([PGP signature](litmus-0.9.2.tar.gz.asc))

*   Fix build when configured without SSL support.
*   Fix build on FreeBSD.

#### Changes in release [litmus 0.9.1](litmus-0.9.1.tar.gz), 17 March 2003 ([PGP signature](litmus-0.9.1.tar.gz.asc))

*   Fix build with bundled copy of expat.
*   Tweaks to conditional PUT tests (Julian Reschke).

#### Changes in release [litmus 0.9](litmus-0.9.tar.gz), 16 March 2003 ([PGP signature](litmus-0.9.tar.gz.asc))

*   New tests submitted by Julian Reschke:
    *   check handling of high Unicode values in property values
    *   check handling of resource URIs including non-ASCII characters
*   Implement Julian's conditional PUT tests, testing If: headers with various combinations of lock-tokens and etags.
*   Add test for Apache 2.0 namespace handling bug #14969.
*   Fix use of proxy with non-default port.

#### Changes in release [litmus 0.8](litmus-0.8.tar.gz), 26 August 2002 ([PGP signature](litmus-0.8.tar.gz.asc))

*   Persistent connections are enabled by default.
*   Updated to neon 0.23.0:
    *   many SSL fixes and improvements
    *   IPv6 support when getaddrinfo() is detected

#### Changes in release [litmus 0.7](litmus-0.7.tar.gz), 1 May 2002 ([PGP signature](litmus-0.7.tar.gz.asc))

*   Updated to neon 0.20.0:
    *   better handling of LOCK responses for shared locks; use the lock token from the Lock-Token header (not really in 0.6 as claimed).

#### Changes in release [litmus 0.6.1](litmus-0.6.1.tar.gz), 19 March 2002 ([PGP signature](litmus-0.6.1.tar.gz.asc))

*   Better chance of compiling on cygwin.

#### Changes in release [litmus 0.6](litmus-0.6.tar.gz), 19 March 2002 ([PGP signature](litmus-0.6.tar.gz.asc))

*   Fixes for cygwin (thanks to Julian Reschke).
*   Improved failure messages.
*   If a LOCK fails, dependant tests will be skipped.
*   Add documentation to 'FAQ' on some of the tests which failed with mod\_dav 1.0.2.
*   Upgrade to neon 0.20.0-dev:
    *   better handling of LOCK responses for shared locks; use the lock token from the Lock-Token header.
    *   RFC2518 compliance fix: use absoluteURIs in If: headers

#### Changes in release [litmus 0.5](litmus-0.5.tar.gz), 5 January 2002 ([PGP signature](litmus-0.5.tar.gz.asc))

*   Fix authentication.
*   Add support for proxy servers using \`--proxy=hostname:port' option.
    *   from build tree, use 'make OPTS="--proxy=hostname:port" URL="..." check'
*   Add -k/--keep-going option to 'litmus' script, to have testing continue even after a test program fails.

#### Changes in release [litmus 0.4](litmus-0.4.tar.gz), 5 January 2002 ([PGP signature](litmus-0.4.tar.gz.asc))

*   Renamed project from "neon-interop" to "litmus".
*   Greatly improved error messages for test failures throughout.
*   Add locking tests (portions from Chris Sharp):
    *   modifying a locked resource as and not as lock owner
    *   shared and exclusive locks, lock discovery
    *   lock doesn't follow COPY
*   Tests are run in a new, empty collection: eliminate problems caused by left-over files from previous failed runs.
*   Add tests for MKCOL on plain resource, with strange body.
*   Each request will have a request header 'X-Litmus' giving the test number and description, to aid debugging using network trace tools.
*   Tests separated into several executables. Can easily run a subset of tests now using e.g. 'make TESTS=locks URL=http://blah/ check'
*   Add 'litmus' wrapper script and 'make install' target.
*   Based on neon 0.18: brings portability fixes, etc.

#### Changes in release [neon-interop 0.3](neon-interop-0.3.tar.gz), 3 November 2001 ([PGP signature](neon-interop-0.3.tar.gz.asc))

*   Add tests for "empty namespace" bugs found in mod\_dav by Julian Reschke.
*   Add tests for properties in many namespaces.

#### Changes in version [neon-interop 0.2](neon-interop-0.2.tar.gz), 15 October 2001

*   Catch up with neon 0.17 test framework, beautify output.

#### Changes in version [neon-interop 0.1](neon-interop-0.1.tar.gz), 12 August 2001

*   Added check for "Expect: 100-continue" support.

#### Changes in version neon-interop-0.0

*   Initial version used at the WebDAV Interoperability Event in UC Santa Cruz, July 19-20th 2001.

* * *

[Joe Orton](mailto:joe@manyfish.co.uk)