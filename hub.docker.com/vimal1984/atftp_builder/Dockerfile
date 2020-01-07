FROM    opensuse/leap:latest
LABEL   maintainer="vimalkrishna84@gmail.com"
LABEL   description="The purpose of this image is to compile the source code of atftp"
LABEL   usage="docker run --rm -v <path to source atftp.rpm>:/src/atftp.rpm -v <directory on host to place the RPM>:/usr/src/packages/RPMS/x86_64 opensuse_atftp_builder"
RUN     zypper addrepo -G -f https://download.opensuse.org/repositories/devel:gcc/openSUSE_Leap_15.1/devel:gcc.repo
RUN     zypper mr -d repo-update
RUN     zypper refresh
RUN     zypper install -y rpm-build
RUN     zypper install -y pcre-devel
RUN     zypper install -y readline-devel
RUN     zypper install -y tcpd-devel
RUN     zypper install -y autoconf automake perl-CPAN-Mini gcc48
RUN     export PERL_MM_USE_DEFAULT=1; perl -MCPAN -e 'install threads::shared'
RUN     rm /usr/bin/gcc; ln -s /usr/bin/gcc-4.8 /usr/bin/gcc
RUN     mkdir /scripts
COPY    build.sh /scripts
WORKDIR /scripts
CMD     ["bash", "build.sh"]
