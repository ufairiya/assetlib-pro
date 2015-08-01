AssetLib Pro uses code from AssetLib (http://codeigniter.com/forums/viewthread/74659/), but does not have much in common with AssetLib anymore.

In addition to AssetLib's **jsmin** and **csstidy** functionality AssetLib Pro brings you the following:
  1. It **fixes relative url() paths** in your css files to **ensure their validity**.
  1. It has a **smart versioning mechanism**:
    1. It **re-creates compressed files automatically** once a source file was changed making sure that your cached files are **always up-to-date**.
    1. It sets **HTTP headers** for far-future caching expiration for **forced browser caching**.
    1. It supports branching for the use of **multiple CSS selections** (like "**screen**" or "**print**").
    1. It allows you to use **multiple sets** of css/js files per CI application for **minimized performace overhead**.
  1. It supports **GZip compression** of cached files to take **bandwidth optimization** a step further.

# Documentation of InstallationAndConfiguration #

## Update: v1.0.4 http://code.google.com/p/assetlib-pro/downloads/detail?name=Assetlibpro_1.0.4.php ##

# Known issues: #
When error report is set to E\_ALL you might get an “Uninitialized string offset” error from CSSTidy.  I’m just pointing this out here since CSSTidy is apparently no longer maintained and it might help someone here.  As far as I can tell, when the first line of my first css file begins with “/**”
```
/*
* Some comment here
*/
```
the index (i) the first time csstidy’s escape function is entered is zero instead of 1.  Zero throws the warning.  There is an error suppression operator, but it appears to not work even though php.net appears to claim that bug was fixed a couple of years ago.  So anyway, problem is resolved if you don’t have error notices or if you don’t have “/**” as the first line (I just added a blank line and all is well).

_(Thanks for a&w for pointing out this issue with CSSTidy)_