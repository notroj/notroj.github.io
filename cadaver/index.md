---
title: cadaver
tagline: A command-line WebDAV client
---

_cadaver_ is a command-line WebDAV client for Unix. It supports file
upload, download, on-screen display, namespace operations (move/copy),
collection creation and deletion, and locking operations.

cadaver is free software, distributed under the GNU GPL. 

* * *

*   [Github repository](https://github.com/notroj/cadaver)
*   [Discussion forum](https://github.com/notroj/cadaver/discussions)
*   [Bug reports](https://github.com/notroj/cadaver/issues)

* * *

#### Changes in release 0.26 ([cadaver-0.26.tar.gz](cadaver-0.26.tar.gz)), 27 November 2024

* Argument passed to "cadaver" must now be an absolute URI,
  various pseudo-URLs are now treated as errors.
* Rewrite of path and character set handling, fixing support
  for locales using non-UTF-8 character encoding:
  * URI paths are translated to/from the native character encoding
  * nl_langinfo() used to detect UTF-8 locale support
  * full relative path resolution is now done for paths
  * "get" now uses a locale-native default filename (issue #33)
  * iconv (or libiconv) is required for non-UTF-8 native locales
* Fix memory leak in remote filename completion.
* Various commands will now automatically act on the destination
  of a redirect as required rather than failing.
* Rewrite of 'copy' and 'move' commands:
  * a source collection is moved/copied inside a destination coll
   rather than overwriting it.
  * more error cases are disallowed (e.g. 'mv / /foo')
  * a source collection with a non-collection destination now fails
* New 'rename' command added for MOVE with 'Overwrite: F'
  * this ignores the 'overwrite' boolean option unlike cp/mv
* Various minor command fixes:
  * propget: output improved for clarity.
  * rmcol: lock handling on error path fixed.
  * less: catch errors from pager command.
* Added 'systemproxy' option to enable libproxy.
* Update to neon 0.34.0

#### Changes in release 0.24 ([cadaver-0.24.tar.gz](cadaver-0.24.tar.gz)), 30 October 2022

* Modernize configure scripts (Hugh McMaster)
 * fixing cross-compilation support
* Various spelling fixes (Hugh McMaster)
* Cosmetic fix for "cat" output
* Bundled neon support is not supported
* Support building against neon up to 0.32

#### Changes in release 0.23.3 ([cadaver-0.23.3.tar.gz](cadaver-0.23.3.tar.gz)), 15 December 2009

* Update to neon 0.29.1.

* * *

[Joe Orton](mailto:joe@manyfish.co.uk)
