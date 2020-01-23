FROM ubuntu:bionic
MAINTAINER ASCDC <asdc.sinica@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN mkdir /script
ADD run.sh /script/run.sh

RUN chmod +x /script/*.sh && \
	apt-get update && \
	DEBIAN_FRONTEND=noninteractive && \
	apt-get -yqq install sudo apt-utils software-properties-common locales language-pack-zh-hant language-pack-zh-hant-base && \
	echo "locales locales/default_environment_locale select zh_TW.UTF-8" | debconf-set-selections && \
	echo "locales locales/locales_to_be_generated multiselect zh_TW.UTF-8 UTF-8" | debconf-set-selections && \
	rm "/etc/locale.gen" && \
	dpkg-reconfigure --frontend noninteractive locales && \
	apt-add-repository -y ppa:ondrej/php && \
	apt-add-repository -y ppa:ondrej/apache2
RUN DEBIAN_FRONTEND=noninteractive && apt-get update && \
	apt-get -y upgrade && \
	apt-get install -y apache2 php7.3 php7.3-common php7.3-json php7.3-opcache php-uploadprogress php-memcache php7.3-zip php7.3-mysql php7.3-phpdbg php7.3-gd php7.3-imap php7.3-ldap php7.3-pgsql php7.3-pspell php7.3-recode php7.3-tidy php7.3-dev php7.3-intl php7.3-curl php7.3-xmlrpc php7.3-xsl php7.3-bz2 php7.3-mbstring pkg-config libmagickwand-dev imagemagick build-essential && \
	echo 'autodetect'|pecl install imagick && \
	echo "extension=imagick.so" | sudo tee /etc/php/7.3/mods-available/imagick.ini && \
	ln -sf /etc/php/7.3/mods-available/imagick.ini /etc/php/7.3/apache2/conf.d/20-imagick.ini && \
	ln -sf /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/rewrite.load

EXPOSE 80
WORKDIR /var/www/html
ENTRYPOINT ["/script/run.sh"]
