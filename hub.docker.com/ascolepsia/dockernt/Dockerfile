FROM ubuntu:trusty
MAINTAINER ASCDC <asdc.sinica@gmail.com>

ADD run.sh /run.sh
ADD locale.gen /etc/locale.gen
ADD locale-archive /usr/lib/locale/locale-archive

RUN chmod +x /*.sh && \
	apt-get update && \
	DEBIAN_FRONTEND=noninteractive && \
	apt-get -y install locales software-properties-common python-software-properties wget curl vim git && \
	echo "alias ll='ls -al'" >> /root/.profile && \
	echo "export LANG=zh_TW.UTF-8" >> /root/.profile && \ 
	echo "export LANGUAGE=zh_TW" >> /root/.profile && \
	echo "export LC_ALL=zh_TW.UTF-8" >> /root/.profile && \
	locale-gen zh_TW.UTF-8 && \
	dpkg-reconfigure locales && \
	export LANG=zh_TW.UTF-8 && \
	add-apt-repository -y ppa:ondrej/php && \
	add-apt-repository -y ppa:ondrej/apache2
	
RUN DEBIAN_FRONTEND=noninteractive && apt-get update && \
	apt-get -y upgrade && \
	apt-get install -y ^apache2$ ^php7\.2$ ^php7\.2-common$ ^php7\.2-json$ ^php7\.2-opcache$ ^php7\.2-zip$ ^php7\.2-mysql$ ^php7\.2-phpdbg$ ^php7\.2-gd$ ^php7\.2-imap$ ^php7\.2-ldap$ ^php7\.2-pgsql$ ^php7\.2-pspell$ ^php7\.2-recode$ ^php7\.2-tidy$ ^php7\.2-intl$ ^php7\.2-curl$ ^php7\.2-xmlrpc$ ^php7\.2-imagick$ ^php7\.2-xsl$ ^php7\.2-bz2$ ^php7\.2-mbstring$ pkg-config libmagickwand-dev imagemagick build-essential libsasl2-dev libpcre3-dev && \
	ln -s ../mods-available/rewrite.load /etc/apache2/mods-enabled/rewrite.load
	
	
ENV LANG zh_TW.UTF-8  
ENV LANGUAGE zh_TW
ENV LC_ALL zh_TW.UTF-8	
	
EXPOSE 80
WORKDIR /var/www/html
ENTRYPOINT ["/run.sh"]