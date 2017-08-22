# Building irssi on OSX

I had problems with the Homebrew version of irssi on my work laptop. I use Perl
locallib, so I wasn't able to run any Perl scripts to customize irssi.

The solution is to compile irssi from source. This runs into a couple of
hurdles because we also need to point the configure script to the system
openssl libs. This is the complete configure command we need:

    $ git clone https://github.com/irssi/irssi
    $ cd irssi
    $ CPPFLAGS=-I/usr/local/opt/openssl/include \
        LDFLAGS=-L/usr/local/opt/openssl/lib \
        ./configure \
            --with-perl=yes \
            --with-perl-lib=~/perl5/lib/perl5 \
            --with-socks \
            --with-bot \
            --with-proxy \
            --prefix=$HOME/Applications/irssi

We don't need the final `--prefix`, but I figure why not since we're already
doing custom things.
