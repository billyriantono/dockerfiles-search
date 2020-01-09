# vim:set ft=dockerfile:
FROM debian:jessie-slim

MAINTAINER Andrius Kairiukstis <andrius@kairiukstis.com>

RUN export DEBIAN_FRONTEND=noninteractive; \
echo "APT::Install-Recommends "false";" > /etc/apt/apt.conf; \
echo "APT::Install-Suggests "false";" >> /etc/apt/apt.conf; \
apt-get update; \
apt-get install -yqq \
  openssl \
  ca-certificates \
  curl \
  wget \
  git \
  subversion; \
cd /usr/src; \
curl -sf -o asterisk.tar.gz -L http://downloads.asterisk.org/pub/telephony/asterisk/asterisk-13-current.tar.gz; \
tar -zxvf asterisk.tar.gz; \
rm asterisk.tar.gz; \
cd asterisk*; \
echo 'Y' | contrib/scripts/install_prereq install; \
contrib/scripts/install_prereq install-unpackaged; \
./configure; \
make all; \
make install; \
make samples; \
make config; \
make install-logrotate; \
cp ./contrib/scripts/astcli /usr/local/bin/; \
mkdir -p /var/spool/asterisk/fax; \
mkdir -p /var/punchblock/record; \
update-rc.d asterisk defaults; \
PACKAGES=`dpkg -l|grep '\-dev'|awk '{print $2}'|xargs`; \
apt-get -yqq purge git subversion wget build-essential; \
apt-get -yqq purge ${PACKAGES}; \
asterisk; \
sleep 5; \
pkill -9 asterisk; \
find /var/log/asterisk/ -type f | xargs rm; \
cd ..; \
rm -rf asterisk*; \
apt-get clean all; \
rm -rf /var/lib/apt/lists/* /usr/share/doc /usr/share/man* /tmp/* /var/tmp/*

ADD docker-entrypoint.sh /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["/usr/sbin/asterisk", "-vvvdddf", "-T", "-W", "-U", "root", "-p"]
