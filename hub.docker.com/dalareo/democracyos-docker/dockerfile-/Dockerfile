FROM centos:7

# Prerequisites
RUN yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
                   https://mirror.webtatic.com/yum/el7/webtatic-release.rpm

# System dependencies
RUN yum install -y ImageMagick \
                   httpd \
                   php72w php72w-cli php72w-common php72w-devel php72w-embedded php72w-fpm php72w-gd php72w-mbstring php72w-mysqlnd php72w-opcache php72w-pdo php72w-xml \
                   curl bzip2 zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gcc make libffi-devel && \
    yum clean all -y
    
# Python3
ENV PYTHON_VERSION 3.7.4
RUN curl -fSL "https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tgz" -o Python.tgz \
	&& tar -xz -f Python.tgz \
	&& cd Python-${PYTHON_VERSION} \
#	&& rm Python.tgz \
	&& ./configure \
	&& make \
	&& make install
    
# SQLite Directory Setup
RUN mkdir -p /var/www/data \
    && chown -R apache:apache /var/www/data \
    && chown -R apache:apache /var/www/html

#USER apache

WORKDIR /var/www/html

# Version
ENV MEDIAWIKI_MAJOR_VERSION 1.32
ENV MEDIAWIKI_VERSION 1.32.3
# ENV MEDIAWIKI_SHA512 79f13245fe2a8851780ac9f38c3f439a4911f6760e810712922b18c577e3ee6e4b0f3e336c567f6115258aebd5fc5e7c6c1045f43b5d0f615bfdcfb54fd16335

# MediaWiki setup
RUN curl -fSL "https://releases.wikimedia.org/mediawiki/${MEDIAWIKI_MAJOR_VERSION}/mediawiki-${MEDIAWIKI_VERSION}.tar.gz" -o mediawiki.tar.gz \
#	&& echo "${MEDIAWIKI_SHA512} *mediawiki.tar.gz" | sha512sum -c - \
	&& tar -xz --strip-components=1 -f mediawiki.tar.gz \
	&& rm mediawiki.tar.gz \
	&& chown -R apache:apache extensions skins cache images

# MediaWiki setup
RUN curl -fSL "https://wiki.openstreetmap.org/osm_logo_wiki.png" -o resources/assets/wiki.png

# Extension:Math
ENV MATH_VERSION REL1_32-b976708
RUN curl -fSL "https://extdist.wmflabs.org/dist/extensions/Math-${MATH_VERSION}.tar.gz" -o Math.tar.gz \
	&& tar -xz -f Math.tar.gz -C extensions \
	&& rm Math.tar.gz \
	&& chown -R apache:apache extensions skins cache images

# Extension:Translate
ENV LANGUAGE_VERSION 2019.04
RUN curl -fSL "https://translatewiki.net/mleb/MediaWikiLanguageExtensionBundle-${LANGUAGE_VERSION}.tar.bz2" -o MediaWikiLanguageExtensionBundle.tar.bz2 \
	&& tar -xj -f MediaWikiLanguageExtensionBundle.tar.bz2 \
	&& rm MediaWikiLanguageExtensionBundle.tar.bz2 \
	&& chown -R apache:apache extensions skins cache images
	
ADD LocalSettings.php LocalSettings.php
RUN echo "ServerName 0.0.0.0:80" >> /etc/httpd/conf/httpd.conf

EXPOSE 80

ENTRYPOINT ["/usr/sbin/httpd", "-DFOREGROUND"] 