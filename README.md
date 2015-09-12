Peter Selinger: ccrypt [ ![](images/software.gif)
](http://www.mathstat.dal.ca/~selinger/software.html) [
http://www.mathstat.dal.ca/~selinger/

# ccrypt

Secure encryption and decryption of files and streams

* * *

I love ccrypt; it is easy to use and does exactly what one wants from an
enrcyption program. Furthermore it's quite fast. It's a wonder the program
isn't more widely known. (Jean-Yves Sireau, Hong Kong)  


### Description

**ccrypt** is a utility for encrypting and decrypting files and streams. It was designed as a replacement for the standard unix crypt utility, which is notorious for using a very weak encryption algorithm. **ccrypt** is based on the Rijndael block cipher, a version of which is also used in the Advanced Encryption Standard (AES, see <http://www.nist.gov/aes>). This cipher is believed to provide very strong security. 

Unlike unix crypt, the algorithm provided by **ccrypt** is not symmetric,
i.e., one must specify whether to encrypt or decrypt. The most common way to
invoke **ccrypt** is via the commands **ccencrypt** and **ccdecrypt**. There
is also a **ccat** command for decrypting a file directly to the terminal,
thus reducing the likelihood of leaving temporary plaintext files around. In
addition, there is a compatibility mode for decrypting legacy unix crypt
files. An emacs mode is also supplied for editing encrypted text files.

Encryption and decryption depends on a keyword (or key phrase) supplied by the
user. By default, the user is prompted to enter a keyword from the terminal.
Keywords can consist of any number of characters, and all characters are
significant (although **ccrypt** internally hashes the key to 256 bits).
Longer keywords provide better security than short ones, since they are less
likely to be discovered by exhaustive search.

For a detailed description of the encryption algorithm used by **ccrypt**, see
the [man page](ccrypt.html).

### Frequently Asked Questions

I often receive questions from users about ccrypt. I have written up the
answers to some [Frequently Asked Questions](faq.html).

### News

For changes prior to version 1.8, see the file [NEWS](NEWS). For a more
detailed list of changes, see the [ChangeLog](ChangeLog).

**October 18, 2012: Release 1.10.** This release fixes a number of minor portability issues and minor bugs. The ccrypt core functionality has been factored into a convenience library libccrypt.a. A ccguess program was added to assist in the recovery of mistyped keys. Improved error checking and fixed minor compiler warnings. Minor improvements to emacs support, and added a --disable-emacs configuration option. Thanks to bornlibra23 and Johannes Ruscheinski for bug reports. 

**August 28, 2009: Release 1.9.** This release fixes a number of portability issues. There is no change in functionality relative to release 1.8. However, compilation errors on several platforms have been fixed, including Mac OSX, Ubuntu, FreeBSD, and Solaris 10. Also, rudimentary OS/2 support via EMX has been added. Thanks to Lester Ingber, Elbert Pol, and Michael Annino for reporting problems and helping to fix them. 

**June 5, 2009: Release 1.8.** This long-overdue release fixes some minor bugs and adds minor features. Added a new --keyref option to avoid double password prompt. Added a new exit code in case the key was not entered or not found. Added internationalization support and German and French translations. Fixed minor bugs in user interface and updated emacs support. Password files ending in a DOS-style end-of-line marker are now correctly recognized. Improved portability and testing. 

### Downloading and Installing

You have three different options for installing ccrypt:

  1. **From source**. Download the "source distribution" from the below list of downloads. Ccrypt is built from sources using the standard configure/make commands. Please see the file [INSTALL](INSTALL) for detailed instructions. 
  2. **From a precompiled binary distribution**. Precompiled distributions are available for a number of platforms; please download the one you need from the below list. Note that some binary distributions are of older versions of ccrypt. See the file [README](README) for some hints on how to install the binaries. Windows users please see the file [README.win](README.win). 
  3. **From a package**. These are for specific platforms. If you want to use one of these, you probably know how.  If you would like to ensure the accuracy of the downloaded files, you can double-check their [SHA1 sums](download/SHA1SUMS). 

Source distribution:

    
    
    ccrypt 1.10. Secure encryption and decryption of files and streams.
    
    Usage: ccrypt [mode] [options] [file...]
           ccencrypt [options] [file...]
           ccdecrypt [options] [file...]
           ccat [options] file...
    
    Modes:
        -e, --encrypt         encrypt
        -d, --decrypt         decrypt
        -c, --cat             cat; decrypt files to stdout
        -x, --keychange       change key
        -u, --unixcrypt       decrypt old unix crypt files
    
    Options:
        -h, --help            print this help message and exit
        -V, --version         print version info and exit
        -L, --license         print license info and exit
        -v, --verbose         print progress information to stderr
        -q, --quiet           run quietly; suppress warnings
        -f, --force           overwrite existing files without asking
        -m, --mismatch        allow decryption with non-matching key
        -E, --envvar var      read keyword from environment variable (unsafe)
        -K, --key key         give keyword on command line (unsafe)
        -k, --keyfile file    read keyword(s) as first line(s) from file
        -P, --prompt prompt   use this prompt instead of default
        -S, --suffix .suf     use suffix .suf instead of default .cpt
        -s, --strictsuffix    refuse to encrypt files which already have suffix
        -F, --envvar2 var     as -E for second keyword (for keychange mode)
        -H, --key2 key        as -K for second keyword (for keychange mode)
        -Q, --prompt2 prompt  as -P for second keyword (for keychange mode)
        -t, --timid           prompt twice for encryption keys (default)
        -b, --brave           prompt only once for encryption keys
        -y, --keyref file     encryption key must match this encrypted file
        -r, --recursive       recurse through directories
        -R, --rec-symlinks    follow symbolic links as subdirectories
        -l, --symlinks        dereference symbolic links
        -T, --tmpfiles        use temporary files instead of overwriting (unsafe)
        --                    end of options, filenames follow
    

For detailed usage information, see the [man page](ccrypt.html).

### Emacs Support

**ccrypt** comes with an emacs package for reading and writing encrypted files. (Note that this package currently only works with emacs, not with xemacs.) The package is called ps-ccrypt, and it is based directly on the jka-compr package which is part of GNU Emacs. Unlike previous versions of this package, it can be used in addition to, and not instead of, jka-compr, to handle both encrypted and compressed files. (However, files that are both encrypted and compressed are not currently handled correctly). 

To use the package, simply load ps-ccrypt and edit as usual. When you open a
file with the ".cpt" extension, emacs will prompt you for a password for the
file. It will remember the password for the buffer, and when you save the file
later, it will be automatically encrypted again (provided you save it with a
".cpt" extension). Except for the password prompt, the operation of the
package should be transparent to the user. The command M-x ccrypt-set-buffer-
password can be used to change the current password of a buffer.

The simplest way to use this package is to include the lines

    
    
    (setq load-path (cons "_path_" load-path))
    (require 'ps-ccrypt "ps-ccrypt.el")
    

in your .emacs file, where _path_ is the directory which holds the file ps-
ccrypt.el.

### Other software related to ccrypt

The following is a list of software related to ccrypt. The list is not
comprehensive; please let me know if you know of other such programs. Note
that I have not tried most of these programs. Use them at your own risk.

  * **[gjots](http://bhepple.freeshell.org/gjots/)** by Bob Hepple. A lightweight jotter which marshals and organizes text notes in a convenient, hierarchical way. It can be used for notes, jottings, bits and pieces, recipes, and even PINs and passwords (encrypted with ccrypt). (Added Oct 2, 2003). 
  * **[xzgvz](download/xzgvz-0.8z.tar.bz2)** by Stan Zitello. A modification of [xzgv](http://web.archive.org/web/20040716075118/http://xzgv.browser.org/), a GTK-based image viewer. The modified version can display ccrypt-encoded jpeg images with the filename extensions .cjpg or .cjpeg. (Added Jan 30, 2004). 
  * **[Ccrypt-GUIs Integration Scripts](VF/README.html)** by VF. A collection of scripts for creating context menu entries for ccrypt in KDE, Gnome, and Windows 98+. This should allow you to encrypt/decrypt files by right-clicking on them. (Added Sep 26, 2004). 
  * **[Tkccrypt](http://vicerveza.homeunix.net/~viric/soft/tkccrypt/)** by Lluis Batlle i Rossell. A simple text editor for ccrypt'ed files. (Added Nov 2, 2006). 
  * **[Qccrypt](http://qccrypt.free.fr/)** by Philippe Beaureilles. This is a cross-platform graphical user interface for ccrypt. It works anywhere QT is available, like Linux, Windows, and Mac. (Added Apr 3, 2011). 
  * **[CCRYPTGUI](http://www.softwaremustbefree.eu/en/ccryptgui/)** by Martin Hilscher. Another graphical user interface for ccrypt using QT. Works in English or German. (Added Apr 3, 2011). 
  * **[Antigift](http://sourceforge.net/p/antigift/wiki/Home/)** by Maxim Falcony. A simple cross-platform encryption tool. (Added Aug 8, 2012). 

### Support and Reporting Bugs

![Get ccrypt at

 SourceForge.net. Fast, secure and Free Open Source software

 downloads](http://sflogo.sourceforge.net/sflogo.php?group_id=40913&type=14)
Ccrypt has a project page on
[SourceForge](http://sourceforge.net/projects/ccrypt/). There, you will find
facilities for reporting bugs, submitting patches, asking for support, asking
for features, or discussing ccrypt in general. You are encouraged to use these
facilities. You can also send email to the author.

### Sponsored Links

  * [Busybits](http://www.busybits.com/). Human edited web directory since 2005. 

### Version

1.10

### Author

Copyright (C) 2000-2012 Peter Selinger.

### License

This program is free software; you can redistribute it and/or modify it under
the terms of the GNU General Public License as published by the Free Software
Foundation; either version 2, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT
ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS
FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with
this program; if not, write to the Free Software Foundation, Inc., 59 Temple
Place, Suite 330, Boston, MA 02111-1307, USA.

  
Back to Homepage: [
![\[home\]](images/homebutton.gif)](http://www.mathstat.dal.ca/~selinger/)

* * *

[ Peter Selinger](http://www.mathstat.dal.ca/~selinger/) / Department of
Mathematics and Statistics / Dalhousie University  
[selinger@users.sourceforge.net](mailto:selinger@users.sourceforge.net) / [PGP
key](gpg-key.txt) ![](http://counter.digits.com/wc/-d/4/ccrypt)
