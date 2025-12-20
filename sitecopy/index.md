# sitecopy

sitecopy is for easily maintaining remote web sites. The program will upload files to the server which have changed locally, and delete files from the server which have been removed locally, to keep the remote site synchronized with the local site with a single command.

If you want to find out whether this program is for you, try: [Should I Use sitecopy?](why.html). Also, find out about [sitecopy and WebDAV](dav.html).

sitecopy is [free software](http://www.gnu.org/philosophy/free-sw.html), distributed under the GNU GPL.

Patches, bug reports, questions etc. can be reported to the sitecopy [mailing list](http://lists.manyfish.co.uk/mailman/listinfo/sitecopy) (for which a [web archive](http://lists.manyfish.co.uk/pipermail/sitecopy/) is also available).

---

### Current Release
Version: **0.16.6**.

* **Source code, via HTTP**: [sitecopy-0.16.6.tar.gz](sitecopy-0.16.6.tar.gz)
* **GitHub repository**: [Link](https://github.com/notroj/sitecopy/)

---

### Changelog Summary

#### Changes in release [0.16.6](sitecopy-0.16.6.tar.gz) (16 July 2008)
* DAV: Fix crash with progress bar enabled with neon 0.27/0.28.

#### Changes in release [0.16.5](sitecopy-0.16.5.tar.gz) (16 July 2008)
* DAV: Fix SSL cert caching to avoid repeated prompts.
* Update to neon 0.28.3 and support neon 0.24.x through 0.28.x.

#### Changes in release [0.16.3](sitecopy-0.16.3.tar.gz) (12 March 2006)
* DAV: Add PKCS#12 client cert support; "client-cert /path/to/cert.p12".
* Update to neon 0.26.0 (0.24.x and 0.25.x still supported).

#### Changes in release [0.16.2](sitecopy-0.16.2.tar.gz) (30 December 2005)
* Fix over-eager move/rename algorithm when handling a delete of one of a set of identical files.
* DAV: Fix ordering issues with --fetch.
* FTP: Retry after response timeouts for STOR commands.
* Update to neon 0.25.4.

#### Changes in release [0.16.1](sitecopy-0.16.1.tar.gz) (24 September 2005)
* FTP: Fix crash in FTP timeout handling.
* Improve error messages from LIST parser failure.

#### Changes in release [0.16.0](sitecopy-0.16.0.tar.gz) (7 August 2005)
* Fetch mode now fetches a single directory at a time to support specific DAV and FTP server restrictions.
* Updated delete/directory creation order to allow replacing files with directories.
* sftpdriver.c compile fix for older Unixes.
* German translation fix (Jens Seidel).

---
[Historic releases](history.html) | [Joe Orton](mailto:joe@manyfish.co.uk)
