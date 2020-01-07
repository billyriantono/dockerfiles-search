# set base os
FROM linuxserver/baseimage
RUN rm -rf /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh

MAINTAINER Mark Burford <sparklyballs@gmail.com>

# Set correct environment variables
ENV DEBIAN_FRONTEND noninteractive 
ENV HOME /root 
ENV TERM screen
ENV LANG en_US.UTF-8 
ENV LANGUAGE en_US:en 
ENV LC_ALL en_US.UTF-8

# Use baseimage-docker's init system
CMD ["/sbin/my_init"]

# set ports
EXPOSE 9777/udp 
EXPOSE 8080

# adding some files requiried pre-build stage.
ADD src/ /root/

# set volume
VOLUME /config 

# Set the locale
RUN locale-gen en_US.UTF-8

# set kodi checkout version as variable
RUN kodiCheckout=15.0-Isengard && \

# set build dependencies as variable
buildDeps="build-essential \
zip \
unzip \
yasm \
gawk \
cmake \
wget \
git-core \
autoconf \
libtool \
automake \
autopoint \
swig \
doxygen \
openjdk-7-jre-headless \
gperf \
libsqlite3-dev \
libpcre3-dev \
libtag1-dev \
libbluray-dev \
libjasper-dev \
libmicrohttpd-dev \
libavahi-client-dev \
libxrandr-dev \
libssh-dev \
libsmbclient-dev \
libnfs-dev \
libboost1.54-dev \
python-dev \
libmysqlclient-dev \
libgle3-dev \
libglew-dev \
libass-dev \
libmpeg2-4-dev \
libjpeg-dev \
libflac-dev \
libvorbis-dev \
libgnutls-dev \
libbz2-ocaml-dev \
libtiff5-dev \
libyajl-dev \
libssl-dev \
libxml2-dev \
libxslt-dev \
libiso9660-dev \
libtinyxml-dev \
liblzo2-dev" && \

# set runtime dependencies as variable
runtimeDeps="zip \
libpcrecpp0 \
libtag1-vanilla \
libtag1c2a \
libaacs0 \
libbluray1 \
libjasper1 \
libjpeg-turbo8 \
libjpeg8 \
libmicrohttpd10 \
libavahi-client3 \
libavahi-common-dev \
libdbus-1-dev \
libssh-4 \
libsmbclient \
libnfs1 \
libmysqlclient18 \
libgle3 \
libglew1.10 \
libass4 \
libmpeg2-4 \
libjpeg-turbo8 \
libflac8 \
libogg0 \
libvorbis0a \
libvorbisenc2 \
libvorbisfile3 \
libbz2-ocaml \
libtiff5 \
libtiffxx5 \
libyajl2 \
libxslt1.1 \
libiso9660-8 \
libtinyxml2.6.2 \
liblzo2-2 \
libxrandr2 \
unzip" && \

# update apt
mv /root/excludes /etc/dpkg/dpkg.cfg.d/excludes && \
apt-get update -qq && \

# Install build dependencies
apt-get install \
$buildDeps -qy && \

# fetch source packages
cd /tmp/ && \
git clone https://github.com/xbmc/xbmc.git && \
wget http://curl.haxx.se/download/curl-7.43.0.tar.gz && \

# compile curl
cd /tmp && \
tar xvf curl-* && \
cd curl-* && \
./configure \
--prefix=/usr \
--with-ssl \
--with-zlib && \
make && \
make install && \

# checkout required branch, apply patch(es), configure and build kodi
cd /tmp/xbmc && \
mv /root/headless.patch . && \
git checkout $kodiCheckout && \
git apply headless.patch && \
# Configure, make, install kodi
./bootstrap && \
./configure \
--enable-nfs \
--enable-upnp \
--enable-ssh \
--enable-libbluray \
--disable-debug \
--disable-vdpau \
--disable-vaapi \
--disable-crystalhd \
--disable-vdadecoder \
--disable-vtbdecoder \
--disable-openmax \
--disable-joystick \
--disable-rsxs \
--disable-projectm \
--disable-rtmp \
--disable-airplay \
--disable-airtunes \
--disable-dvdcss \
--disable-optical-drive \
--disable-libusb \
--disable-libcec \
--disable-libmp3lame \
--disable-libcap \
--disable-udev \
--disable-libvorbisenc \
--disable-asap-codec \
--disable-afpclient \
--disable-goom \
--disable-fishbmc \
--disable-spectrum \
--disable-waveform \
--disable-avahi \
--disable-non-free \
--disable-texturepacker \
--disable-pulse \
--disable-dbus \
--disable-alsa \
--disable-hal \
--prefix=/opt/kodi-server && \
make && \
make install && \

# clean build area of no longer required dependencies and build files
apt-get purge -y --remove \
$buildDeps && \
apt-get -y autoremove && \

# install runtime dependencies
apt-get install \
$runtimeDeps -qy && \

# install kodisend and mariadb-server
add-apt-repository ppa:team-xbmc/ppa && \
apt-get update -qq && \
apt-get install \
mariadb-server \
kodi-eventclients-xbmc-send -qy && \

# remove un-needed repositories
add-apt-repository --remove ppa:team-xbmc/ppa && \

# clean up
cd / && \
apt-get clean -y && \
rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# set config of mariadb
RUN sed -i -e 's#\(bind-address.*=\).*#\1 0.0.0.0#g' /etc/mysql/my.cnf && \
sed -i -e 's#\(log_error.*=\).*#\1 /config/databases/mysql_safe.log#g' /etc/mysql/my.cnf && \
sed -i -e 's/\(user.*=\).*/\1 abc/g' /etc/mysql/my.cnf && \
echo '[mysqld]' > /etc/mysql/conf.d/innodb_file_per_table.cnf && \
echo 'innodb_file_per_table' >> /etc/mysql/conf.d/innodb_file_per_table.cnf

#Adduser abc
RUN useradd -u 911 -U -s /bin/false abc
RUN usermod -G users abc

#Adding Custom files
ADD init/ /etc/my_init.d/
ADD services/ /etc/service/
RUN chmod -v +x /etc/service/*/run
RUN chmod -v +x /etc/my_init.d/*.sh
