FROM eboraas/apache-php
MAINTAINER azmodan2k "work@azmodan.com"
# ORIGINAL MAINTAINER Tobias Mandjik "webmaster@leckerbeef.de"
# ORIGINAL MAINTAINER Felix Bartels "felix@host-consultants.de"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -qq -y && apt-get install -qq -y \
    wget \
    apt-utils \
	debconf \
    mysql-server

RUN mkdir -p /root/packages/zarafa \
	&& cd /root/packages/zarafa \
	&& wget -q http://download.zarafa.com/zarafa/drupal/download_platform.php?platform=final/7.2/7.2.5.109/zcp-7.2.5.109-debian-8.0-x86_64-forhome.tar.gz -O- | tar xz --strip-components=1 \
	&& apt-ftparchive packages . | gzip -9c > Packages.gz \
	&& echo "deb file:/root/packages/zarafa /" > /etc/apt/sources.list.d/zarafa.list \
	&& cd /root \
	&& apt-get update -qq -y \
	&& apt-get install -qq -y --force-yes php5-mapi  \
	&& apt-get install -qq -y --force-yes mysql-server zarafa \
	&& apt-get clean \
	&& mkdir -p /root/packages/webapp \
	&& cd /root/packages/webapp \
	&& wget --quiet -p -r -nc -nd -l 1 -e robots=off -A deb --no-check-certificate https://download.zarafa.com/community/final/WebApp/2.2.1/debian-8.0/ \
	&& apt-ftparchive packages . | gzip -9c > Packages.gz \
	&& echo "deb file:/root/packages/webapp /" > /etc/apt/sources.list.d/webapp.list \
	&& cd /root \
	&& apt-get update -qq -y \
	&& apt-get install -qq -y --force-yes zarafa-webapp  \
	&& apt-get install -qq -y --force-yes zarafa-webapp-* \
	&& apt-get clean
