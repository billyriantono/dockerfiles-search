FROM fedora:23
MAINTAINER nathan@nathansamson.be

RUN dnf install -y subversion binutils bzip2 gcc gcc-c++ gawk gettext flex ncurses-devel zlib-devel zlib-static make patch unzip perl-ExtUtils-MakeMaker \
 glibc glibc-devel glibc-static quilt sed sdcc intltool sharutils bison wget openssl-devel openssl which ccache libtool && dnf clean all

RUN useradd openwrt

USER openwrt
