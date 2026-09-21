# sitecopy

sitecopy is for easily maintaining remote web sites. The program will
upload files to the server which have changed locally, and delete
files from the server which have been removed locally, to keep the
remote site synchronized with the local site with a single command.

sitecopy is [free software](http://www.gnu.org/philosophy/free-sw.html), distributed under the GNU GPL.

---

*  [GitHub repository](https://github.com/notroj/sitecopy)
*  [Discussion forum](https://github.com/notroj/sitecopy/discussions)
*  [Bug reports](https://github.com/notroj/sitecopy/issues)
* **Source code, via HTTP**: [sitecopy-0.16.6.tar.gz](sitecopy-0.16.6.tar.gz)
* **GitHub repository**: [Link](https://github.com/notroj/sitecopy/)

---

### Changelog Summary

#### Changes in release 0.17 ([sitecopy-0.17.tar.gz](sitecopy-0.17.tar.gz)), 21 September 2026
- Update to neon 0.37.1; require neon 0.29+.
- Bundled expat, GNOME frontend removed.

##### State file handling improvements

- Store state files in sorted order (Gary Benson)
- Write state file to a temporary file (michel34)
- Interrupted runs now write updated progress state.
- A lock file is used to prevent concurrent runs (Debian #129330, #41).
- Write failures now reported rather than being silently ignored (#47).

##### Other changes

- Various compilation warning fixes.
- Use exit status 0 for --version and --help.
- Allow URL as site name in rcfile.

##### Various options improvements and cleanups

- The "ftp showquit" and "http expect" options are removed; neither
  was ever implemented.  Both are still accepted, and ignored, so
  that existing rcfiles continue to work.
- nooverwrite: an upload failing after the remote file was deleted no
  longer stops later updates uploading it.
- "permissions dir": if setting the permissions of a new directory
  fails, later updates set them, rather than re-creating the
  directory.
- 'tempupload' use a random suffix for the temporary filename, so as
  not to overwrite another file on the server.
- exclude, ignore and ascii patterns which contain a slash, but do
  not begin with one (e.g. "exclude stats/*"), are now matched
  against the filename relative to the site root, and so match
  files; before, they were matched against the base name, and so
  never matched (Debian bug #167277).
  WARNING: such patterns did nothing before, so files they match may
  already have been uploaded, and an excluded file which is on the
  server is DELETED from it by the next update.  If any exclude
  pattern in your rcfile contains a slash without a leading slash,
  check what the first update will do before running it, with
  "sitecopy --list sitename" or "sitecopy --dry-run --update
  sitename".

##### Other changes

- Enable large file support, so that files of 2GB or more are handled
- Fix --verify for sites with subdirectories, which reported every
- --fetch no longer skips directories beyond 1024, and fails if a file

##### FTP

- Add support for FTP over TLS (RFC 4217) with "ftp secure",
  requiring neon 0.37 or later built with SSL support.
- Apply usecwd for MDTM commands.
- Stricter validation of EPSV responses.
- Improve LIST parsing (Haolin Xue, Debian #496988)

##### Other changes

- DAV: Trust the saved server certificate for "http secure" sites.

##### SFTP

- Fix hang on connect against OpenSSH 4.2 and later
  (Agustin Martin Domingo, Debian #337122, #447598)
- Fix error handling (Haolin Xue, Debian #515217, #564462, #742661)
- Document in the man page (Kartik Mistry, Christian Kujau,
   Debian #320586, #405483, #439594)

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
