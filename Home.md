# QtWebKit Reloaded

This is a project aiming to upgrade QtWebKit to modern WebKit code base.

**Update** See blog post for additional details: http://qtwebkit.blogspot.ru/2016/08/qtwebkit-im-back.html

## Why?

If you wonder why do we need QtWebKit when shiny new QtWebEngine is available, please look at our [[use cases list|Use cases of QtWebKit]]

## Interested and ready to help?

Here is our list of [[things you can do to help us|What can you do to help us]]. We will highly appreciate help of any kind!

Master contains exact mirror of upstream WebKit repository at `git://git.webkit.org/WebKit.git`. Things not directly related to Qt port, like MIPS support, are developed against master, and go through code review on webkit.org.

Development of QtWebKit currently happens in `qtwebkit-stable` branch.

## System requirements

The next configurations are going to be supported:

* OS: Linux (desktop and embedded), Windows 7 SP1 and higher, macOS 10.10 and higher
* Compilers:
    * Linux: g++ >= 4.9 (4.8 with FTL JIT and Indexed DB disabled) or clang++
    * Windows: MSVC 2015 or MinGW-w64 5.3 (though any version >= 4.9 should be fine)
* Qt 5.2 (>= 5.4 recommended)

## Build requirements

Depending on your OS, see
* [[Building QtWebKit on Linux]]
* [[Building QtWebKit on Windows]]
* [[Building QtWebKit on OS X]]

## Usage instructions

See [[Using QtWebKit in your project]]

## Contacts
Mailing list: `webkit-qt@lists.webkit.org`

IRC: `#qtwebkit` on `irc.freenode.net`
