FROM debian:stretch

# install packages
ENV DEBIAN_FRONTEND noninteractive

RUN echo deb http://ftp.cz.debian.org/debian/ stretch main > /etc/apt/sources.list
RUN echo deb-src http://ftp.cz.debian.org/debian/ stretch main >> /etc/apt/sources.list
RUN echo deb http://security.debian.org/debian-security stretch/updates main >> /etc/apt/sources.list
RUN echo deb-src http://security.debian.org/debian-security stretch/updates main >> /etc/apt/sources.list
RUN echo deb http://ftp.cz.debian.org/debian/ stretch-updates main >> /etc/apt/sources.list
RUN echo deb-src http://ftp.cz.debian.org/debian/ stretch-updates main >> /etc/apt/sources.list

RUN apt-get update &&  apt-get -y upgrade && \
    apt-get -y --force-yes install openssl dpkg-dev debhelper syslog-ng-core syslog-ng && \
    apt-get -y build-dep pure-ftpd-mysql && \
    mkdir /ftpdata && \
    mkdir /tmp/pure-ftpd-mysql && \
    cd /tmp/pure-ftpd-mysql && \
    apt-get source pure-ftpd-mysql && \
    cd pure-ftpd-* && \
    sed -i '/^optflags=/ s/$/ --without-capabilities/g' ./debian/rules && \
    dpkg-buildpackage -b -uc && \
    dpkg -i /tmp/pure-ftpd-mysql/pure-ftpd-common*.deb && \
    apt-get -y install openbsd-inetd \
    mysql-client && \
    dpkg -i /tmp/pure-ftpd-mysql/pure-ftpd-mysql*.deb && \
    apt-mark hold pure-ftpd pure-ftpd-mysql pure-ftpd-common

# add docker user and group
RUN groupadd -g 999 docker
RUN useradd -u 111 -g 999 -d /dev/null -s /usr/sbin/nologin docker
RUN chown -R docker:docker /ftpdata

# cleanup
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/*

# run mysql configuration creator script
COPY run.sh /run.sh
RUN chmod u+x /run.sh

RUN echo ftp.* /var/log/ftp > /etc/syslog.conf

# entry point
ENTRYPOINT ["/run.sh"]

# define important volumes
VOLUME /ftpdata

# expose important ports
EXPOSE 20 21 30000-30009
