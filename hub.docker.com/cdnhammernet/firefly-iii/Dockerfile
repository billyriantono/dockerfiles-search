FROM bitnami/minideb:stretch

ARG OVERLAY_VERSION="v1.21.7.0"
ARG OVERLAY_ARCH="amd64"
ENV FIREFLY_VERSION 4.7.10


RUN \
    apt update && \
    apt install -y \
	curl \
	tar && \
    curl \
	-o /tmp/s6-overlay.tar.gz \
	-L "https://github.com/just-containers/s6-overlay/releases/download/$OVERLAY_VERSION/s6-overlay-$OVERLAY_ARCH.tar.gz" && \
    tar xfz /tmp/s6-overlay.tar.gz -C / && \
	rm -rf /tmp/* && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/


#install packages
RUN \
    apt update && \
    apt install -y \
	wget \
	apt-transport-https && \
    wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
    echo "deb https://packages.sury.org/php/ stretch main" > /etc/apt/sources.list.d/php.list && \
    apt update && \
    apt install -y \
	nginx \
	cron \
	locales \
	unzip \
	php7.2 \
	php7.2-fpm \
	php7.2-zip \
	php7.2-bcmath \
	php7.2-curl \
	php7.2-gd \
	php7.2-intl \
	php7.2-xml \
	php7.2-ldap \
	php7.2-mbstring \
	php7.2-mysql && \
    mkdir -p /run/php && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/
	

# install Firefly III and dependencies via composer
RUN \
    apt update && \
    apt install -y \
	git && \
    curl -sS https://getcomposer.org/installer | php && \
	mv composer.phar /usr/bin/composer && \
    composer create-project grumpydictator/firefly-iii --no-dev --prefer-dist firefly-iii ${FIREFLY_VERSION} && \
\
    apt remove -y \
	git && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/ && \
    rm -f /usr/bin/composer && \
    rm -rf ~/.composer && \
    rm -rf /tmp/*



#configure locales? dpkg-reconfigure locales but how to do without user input?
RUN \
    apt install -y \
	locales && \
    sed --in-place '/en_US.UTF-8/s/^#//' /etc/locale.gen && \
    locale-gen


RUN \
    groupmod -g 1000 users && \
	useradd -u 911 -U -d /app -s /bin/false abc && \
	usermod -G users abc


COPY root/ /

#VOLUME ["/app/storage","/app/public/logo"]
EXPOSE 80

ENTRYPOINT ["/init"]
