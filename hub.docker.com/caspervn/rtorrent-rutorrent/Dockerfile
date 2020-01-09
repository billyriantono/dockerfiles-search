FROM debian:jessie

# Create user rtorrent
RUN useradd -m -s /bin/bash rtorrent && echo rtorrent:new_password | chpasswd

# Install all dependencies
RUN apt-get update && apt-get -y install openssl git apache2 apache2-utils build-essential libsigc++-2.0-dev \
	libcurl4-openssl-dev automake libtool libcppunit-dev libncurses5-dev libapache2-mod-scgi \
	php5 php5-curl php5-cli libapache2-mod-php5 tmux unzip libssl-dev curl

# Compile xmlrpc-c
RUN cd /tmp \
	&& curl -L https://sourceforge.net/projects/xmlrpc-c/files/Xmlrpc-c%20Super%20Stable/1.39.13/xmlrpc-c-1.39.13.tgz/download -o xmlrpc-c.tgz \
	&& tar zxvf xmlrpc-c.tgz \
	&& mv xmlrpc-c-1.* xmlrpc \
	&& cd xmlrpc \
	&& ./configure --disable-cplusplus \
	&& make \
	&& make install \
	&& cd ..

# Compile libtorrent
RUN cd /tmp \
	&& curl -L http://rtorrent.net/downloads/libtorrent-0.13.6.tar.gz -o libtorrent.tar.gz \
	&& tar -zxvf libtorrent.tar.gz \
	&& cd libtorrent-0.13.6 \
	&& ./autogen.sh \
	&& ./configure \
	&& make \
	&& make install \
	&& cd ..

# Compile rtorrent
RUN cd /tmp \
	&& curl -L http://rtorrent.net/downloads/rtorrent-0.9.6.tar.gz -o rtorrent.tar.gz \
	&& tar -zxvf rtorrent.tar.gz \
	&& cd rtorrent-0.9.6 \
	&& ./autogen.sh \
	&& ./configure --with-xmlrpc-c \
	&& make \
	&& make install \
	&& cd .. \
	&& ldconfig \
	&& mkdir /home/rtorrent/rtorrent-session \
	&& mkdir /downloads \
	&& mkdir /watch


# Install Rutorrent
RUN cd /tmp \
	&& curl -L https://github.com/Novik/ruTorrent/archive/master.tar.gz -o master.tar.gz \
	&& tar -zxvf master.tar.gz \
	&& rm -f /var/www/html/index.html \
	&& mv -f ruTorrent-master/* /var/www/html/ \
	&& rm -rf /var/www/html/plugins/* \
	&& chown -R www-data.www-data /var/www/html/* \
	&& chmod -R 775 /var/www/html/*

COPY 000-default.conf 000-default-auth.conf /etc/apache2/sites-available/
COPY rtorrent.rc /home/rtorrent/.rtorrent.rc
COPY plugins/ /var/www/html/plugins/
COPY startup.sh /

RUN chown -R www-data.www-data /var/www/html \
	&& chown rtorrent.rtorrent /home/rtorrent/.rtorrent.rc /home/rtorrent/rtorrent-session /downloads /watch

VOLUME ["/downloads", "/watch"]

ENTRYPOINT ["/startup.sh"]
