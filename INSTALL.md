# INSTALL for Fluxbox

## TL;DR Instructions

- a) install pre-compiled binary packages via a system package manager

or

- b) compile and install from source code
```
./configure
sudo make
sudo make install
```

## Platforms, packages and installing pre-compiled

Fluxbox is available via the package managers and repositories of many Unix-like systems. 
(See https://pkgs.org/download/fluxbox)

- Unix-based, including FreeBSD and NetBSD
- Linux-based systems (distributions) including Adélie, Alpine, ALT Linux, Arch Linux, Debian, Fedora, Mageia, OpenMandriva, openSUSE, PCLinuxOS, Red Hat Enterprise Linux (RHEL), Slackware, Solus, Ubuntu, Void Linux


Note that Fluxbox development team are not responsible for any package included in your distribution.


- also refer to https://www.addictivetips.com/ubuntu-linux-tips/set-up-the-fluxbox-window-manager-on-linux/ for more installation, **configuration** and use info

### Arch Linux
```
sudo pacman -Sy
sudo pacman -S fluxbox
```

### Debian / antiX / MX / Ubuntu Linux

#### Debian
```
sudo apt-get update
sudo apt-get -y install fluxbox
```

**note**: `apt-get` can be substituted with `apt` or `nala` (`sudo apt install nala` first)

#### antiX

- Fluxbox is included with the "base" and "full" editions

in case of problems with fluxbox on antiX:

check `~/.desktop-session`

and

`~/.fluxbox/startup`

should have this line included / enabled:

`exec /usr/bin/fluxbox`


Check that the following are installed (or re-install)
```
desktop-session-antix
desktop-menu-antix
desktop-defaults-antix
desktop-defaults-fluxbox-antix
```

What do the log files in `~/.desktop-session` show?

Someone had a problem with Fluxbox no longer working on antiX, after they accidentally deleted the shebang line from `~/.fluxbox/startup` while editing the file in vim

- for more info on configuring and using Fluxbox on antiX Linux, see https://download.tuxfamily.org/antix/docs-antiX-23/FAQ/fluxbox.html

#### MX Linux

- Fluxbox is included with the Fluxbox, Xfce and AHS Xfce editions

#### Ubuntu
```
sudo add-apt-repository universe
sudo apt update
sudo apt install fluxbox
```

### Fedora Linux

- see https://fedoraproject.org/wiki/Fluxbox for more info

update package database then install fluxbox package with either `dnf` or `yum`
```
sudo dnf makecache --refresh
sudo dnf -y install fluxbox
```

**note**: `dnf` can be substituted with `yum`

### openSUSE Linux
```
sudo zypper install fluxbox
```

### Slackware Linux
```
slackpkg install fluxbox
```

- At installation time, you can select Fluxbox as your window manager in step **SELECT DEFAULT WINDOW MANAGER FOR X**. 

- Then you can start Fluxbox with X: 
`startx`

- If fluxbox is not your default manager: 
`startfluxbox`

- For an installed system, you can switch between window managers by running the `xwmconfig` script as root: 
`sudo xwmconfig`


for more information and configs:
- also see https://docs.slackware.com/howtos:window_managers:fluxbox
- and https://slackwiki.com/Fluxbox_Newbie

### Void Linux
```
sudo xbps-install -Su fluxbox
```

### FreeBSD

FreshPorts https://www.freshports.org/x11-wm/fluxbox/
- as at 20240612 fluxbox 1.3.7_8 is available for FreeBSD 13, 14, 15
- also listed in the commit history are earlier versions of fluxbox down to 0.1.5


to install the port:
```
cd /usr/ports/x11-wm/fluxbox/ && make install clean
```

to add the package, run one of these commands:
```
pkg install x11-wm/fluxbox
pkg install fluxbox
```

### NetBSD

Packages Collection (pkgsrc) https://cdn.netbsd.org/pub/pkgsrc/current/pkgsrc/wm/fluxbox/index.html

- see http://wiki.netbsd.org/tutorials/x11/fluxbox/ for more installation and configuration info


to install fluxbox, do either of:

- a) install binary package
```
pkgin in fluxbox
```
- **note**: use `pkg_add` to install pkgin first, or directly to install fluxbox


- b) build with pkgsrc
```
cd /usr/pkgsrc/wm/fluxbox
make install
```

- to make it your default window manager, 
edit your `.xinitrc` and change or add the exec instruction on the last line as: 
`exec fluxbox -W` # no '&' here, as at the end of the other lines in .xinitrc


- refer to https://www.netbsd.org/docs/guide/en/chap-x.html


## Compilation and Installation

The `configure` shell script attempts to guess correct values for
various system-dependent variables used during compilation.  It uses
those values to create a `Makefile` in each directory in the
Fluxbox source tree.

Finally, it creates a shell script `config.status` that you can run
in the future to recreate the current configuration, a file
`config.cache` that saves the results of its tests to speed up
reconfiguring, and a file `config.log` containing compiler output
(useful mainly for debugging `configure`).

If you need to do unusual things to compile Fluxbox, please try
to figure out how `configure` could check whether to do them, and mail
diffs or instructions to fluxbox-developers list (see www.fluxbox.org) 
so they can be considered for the next release.  If at some point 
`config.cache` contains results you don't want to keep, you may remove 
or edit it.

The file `configure.in` is used to create `configure` by a program
called `autoconf`.  You only need `configure.in` if you want to change
it or regenerate `configure` using a newer version of `autoconf`.

The simplest way to compile this package is:

1. `cd` to the directory containing the package's source code and enter
`./configure` to configure the package for your system. If you're
using `csh` on an old version of System V, you might need to type
`sh ./configure` instead to prevent `csh` from trying to execute
`configure` itself.

Running `configure` takes a while. While running, it prints some
messages telling which features it is checking for.

2. Enter `make` to compile the package.

3. Enter `make install` to install the programs and any data files and documentation.

4. Remove the program binaries and object files from the source code directory with `make clean`.
5. To also remove the files that `configure` created (so you can compile the package for
a different kind of computer), use `make distclean`. 

## Compilers and Options

Some systems require unusual options for compilation or linking that
the `configure` script does not know about.  You can give `configure`
initial values for variables by setting them in the environment.
Using a Bourne-compatible shell, you can do that on the command line like this:
`CC=c89 CFLAGS=-O2 LIBS=-lposix ./configure`

Or on systems that have the `env` program, you can do it like this:
`env CPPFLAGS=-I/usr/local/include LDFLAGS=-s ./configure`

### Cross-Compiler for Microsoft Windows

You'll want mingw-cross-env installed, with libX11 and mingw-catgets built.

A configure line that works is:

```
./configure \
	--prefix=/ \
	--host=i686-pc-mingw32 \
	--disable-imlib2 \
	--disable-xmb \
	--disable-slit \
	--disable-remember \
	--disable-toolbar \
	--disable-fribidi \
	--disable-nls \
	--disable-xft \
	LIBS="-lxcb -lXdmcp -lXau -lpthread -lws2_32"
```

Then, build and install with
`make install DESTDIR=$(pwd)/stage`

You can then copy the whole "stage" directory to a Windows machine and
run it on your choice of X server.


## Optional Features

Fluxbox supports the XShape extension of X11R6.  This support is enabled by default, 
but may be overridden by specifying `--disable-shape` on the configure script's command line.

Fluxbox supports Window Maker dockapps (warning: restarts from wmaker to
fluxbox don't always handle dockapps correctly) with a gadget called the Slit.
The Slit is compiled into Fluxbox by default, but may be overridden by
specifying `--disable-slit` on the configure script's command line.

Fluxbox supports a rendering effect called "faked interlacing" which darkens
every other line in rendered images.  This support works only for gradient
images.  It is compiled in by default, but may be overridden by specifying
`--disable-interlace` on the configure script's command line.

Fluxbox uses a timer which allows it to periodically flush its pixmap
cache. It is enabled by default, but may be overridden by specifying
'--disable-timed-cache` on the configure script's command line.

Also, `configure` can usually find the X include and library files
automatically, but if it doesn't, you can use the `configure` options 
`--x-includes=DIR` and `--x-libraries=DIR` to specify their locations.

