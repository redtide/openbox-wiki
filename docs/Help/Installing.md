# Installing

## Dependencies

Compiling Openbox should be a relatively painless experience. You will
need the following packages:

- C compiler (such as GCC)
- Libc library and headers (development package)
- Xlib library and headers (development package)
- Xext and Xrandr library and headers (development package) - *optional
  but recommended*
- Glib-2 library and headers (development package)
- LibXML-2 library and headers (development package)
- Pango library and headers (development package)
- Imlib2 (development package) - *optional but recommended*
- Startup-notification library and headers (development package) -
  *optional but recommended*
- XCursor library and headers (development package) - *optional but
  recommended*
- Pkg-config

These should all be available through your distribution.

### Dependencies in Ubuntu and Debian

In Ubuntu and Debian, install the following packages:

- build-essential
- pkg-config
- libpango1.0-dev
- libglib2.0-dev
- libxml2-dev
- libxcursor-dev
- libimlib2-dev
- libstartup-notification0-dev
- xlibs-dev
- libxext-dev
- x11proto-randr-dev

Note: 'xlibs-dev' is no longer available in in Ubuntu 8.04 LTS 'Hardy'
repositories, but 'xlibs-static-dev' is.

If you want to hook in the Debian menu, you'll also want:

- menu
- menu-xdg

### Dependencies in Fedora

In Fedora Core 6 or Fedora 7, install the following packages:

- gcc
- autoconf
- automake
- glib2-devel
- pango-devel
- imlib2-devel
- startup-notification-devel
- libXcursor-devel
- libXfixes-devel
- libSM-devel
- libxml2-devel

## Building and installing the program

Once you have the above dependancies installed, you are ready to build
Openbox.

You can obtain the source code from github.com
or as through tar archives (eg. linux from scratch):

```text
% git clone https://github.com/Mikachu/openbox.git
```

Run bootstrap script to obtain configuration scripts

```text
% ./bootstrap
```

Then run:

```text
% ./configure --prefix=/usr --sysconfdir=/etc
  ...configure detects the build evironment...
% make
  ...openbox builds...
% sudo make install
  ...openbox installs...
```

If you do *not* want to install to `/usr`, then you should use
`./configure --prefix=<whatever you want> --sysconfdir=/etc --datarootdir=/usr/share`.
If you don't do this, the Openbox log in options will not be available,
because they need to be installed to `/usr/share/xsessions`.

If the configure command fails and the reason is not obvious, you should
look in the generated `config.log` file to discover the cause of the
problem.

### For 64-bit distributions

When building Openbox on the 64-bit versions of Debian or Fedora, use:

```text
% ./configure --prefix=/usr --sysconfdir=/etc --libdir=/usr/lib64
% make
% sudo make install
```

### For CentOS 5.3

```text
# yum install automake autoconf glib2-devel pango-devel startup-notification-devel libXcursor-devel libXfixes-devel libSM-devel libxml2-devel gcc-c++.i386 gcc.i386

# ./configure --prefix=/usr --sysconfdir=/etc
# make
# make install
```

### Tips for Developing and Using Openbox at the Same Time

There are several ways of having two xserver sessions at once.

One of these is using Xephyr to create a nested window:

```text
% Xephyr -br -ac -noreset -screen 640x320 :1
```

And then running your second ammended openbox in this display:

```text
% DISPLAY=:1 ./openbox
```

(the line above assumes you're in the directory of where the openbox binaries lie)
