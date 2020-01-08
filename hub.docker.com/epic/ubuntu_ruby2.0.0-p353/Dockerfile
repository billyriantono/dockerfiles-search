#
# Ubuntu and Ruby 2.0.0-p353
#
# In:
#   - OpenSSL
#   - Readline
#   - Zlib
#   - GDBM
#   - FFI
#   - NCurses
#   - Bison
# Out:
#   - Ruby/Tk
#   - Win32 related parts
#   - Documentation from Rdoc
#
# Installed to /usr/local/bin
#

FROM ubuntu

MAINTAINER Eric Platon <zaraki@gmx.com>

# make sure the package repository is up to date
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN apt-get update

# Get necessary packages to build Ruby
RUN apt-get -y install wget gcc make zlib1g-dev openssl libgdbm-dev libreadline6-dev libffi-dev libncurses5-dev libssl-dev libbison-dev

# Get Ruby
RUN wget ftp://ftp.ruby-lang.org/pub/ruby/2.0/ruby-2.0.0-p353.tar.gz
RUN tar xvfz ruby-2.0.0-p353.tar.gz
RUN cd ruby-2.0.0-p353 && ./configure --disable-install-doc && make && make install

# Make Ruby available on the PATH.
RUN export PATH=/usr/local/bin:$PATH