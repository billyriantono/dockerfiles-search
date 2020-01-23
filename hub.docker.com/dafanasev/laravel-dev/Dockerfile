FROM php:alpine
LABEL maintainer="Dmitrii Afanasev <dimarzio1986@gmail.com>"

RUN apk update && apk upgrade && apk add bash 

# install php stuff
RUN apk add --no-cache libpq freetds freetype icu libintl libldap libjpeg libmcrypt libpng libwebp \
	postgresql-dev curl-dev freetds-dev freetype-dev gettext-dev icu-dev jpeg-dev libmcrypt-dev \
	libpng-dev libwebp-dev libxml2-dev openldap-dev \
	&& docker-php-ext-configure gd --with-jpeg-dir=usr/ --with-freetype-dir=usr/ --with-webp-dir=usr/ \
	&& docker-php-ext-configure ldap --with-libdir=lib/ \
	&& docker-php-ext-configure pdo_dblib --with-libdir=lib/ \
	&& /usr/local/bin/pecl download mongodb \
	&& tar -C /usr/src/php/ext -xf mongo*.tgz \
	&& rm mongo*.tgz \
	&& mv /usr/src/php/ext/mongo* /usr/src/php/ext/mongodb \
	&& docker-php-ext-install curl exif gd gettext intl ldap mongodb pdo_dblib pdo_mysql pdo_pgsql xmlrpc zip \
	&& php -r "readfile('https://getcomposer.org/installer');" | php \
	&& mv composer.phar /usr/bin/composer \
	&& chmod +x /usr/bin/composer \
	&& apk del curl-dev freetds-dev freetype-dev gettext-dev icu-dev jpeg-dev libmcrypt-dev \
	  libpng-dev libwebp-dev libxml2-dev openldap-dev postgresql-dev

# Install node stuff
RUN export NODE_VERSION=10.4.1 \
	&& apk add --no-cache curl git make gcc g++ python linux-headers paxctl gnupg libgcc libstdc++ \
  && cd /tmp || exit 1 \
  && curl -o node-v${NODE_VERSION}.tar.xz -sSL https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}.tar.xz \
  && xz -d node-v${NODE_VERSION}.tar.xz \
	&& tar -xf node-v${NODE_VERSION}.tar \
	&& cd node-v${NODE_VERSION} || exit 1 \
	&& export GYP_DEFINES="linux_use_gold_flags=0" \
	&& ./configure --prefix=/usr ${CONFIG_FLAGS} \
	&& NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
	&& make -j${NPROC} -C out mksnapshot BUILDTYPE=Release \
	&& paxctl -cm out/Release/mksnapshot \
	&& make -j${NPROC} \
	&& make install \
	&& paxctl -cm /usr/bin/node \
	&& cd / || exit 1 \
  && git config --global http.sslverify "false" \
  && git clone https://github.com/sass/sassc /sassc \
  && cd /sassc \
  && git clone https://github.com/sass/libsass \
  && SASS_LIBSASS_PATH=/sassc/libsass make \
	&& mv /sassc/bin/sassc /usr/bin/sass \
	&& if [ -x /usr/bin/npm ]; then npm install -g npm@${NPM_VERSION}; find /usr/lib/node_modules/npm -name test -o -name .bin -type d | xargs rm -rf; fi \
	&& rm -rf /etc/ssl /node-${VERSION}.tar.gz /SHASUMS256.txt.asc /node-${VERSION} \
    /usr/share/man /tmp/* /root/.npm /root/.node-gyp /root/.gnupg \
    /usr/lib/node_modules/npm/man /usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html \
    /sassc /usr/include /var/cache/apk/* \
  && apk del git make gcc g++ python linux-headers paxctl gnupg

RUN npm install --ignore-optional -g yarn

# install dockerize
RUN apk add --no-cache ca-certificates wget openssl openssh-client git \
	&& mkdir -p /etc/ssl/certs \
	&& update-ca-certificates \
	&& export DOCKERIZE_VERSION=v0.6.1 \
	&& git config --global http.sslverify "false" \
	&& wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
	&& tar -C /usr/local/bin -xzvf dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
	&& rm dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
	&& apk del ca-certificates wget openssl openssh-client git

WORKDIR /var/www

CMD php ./artisan serve --port=80 --host=0.0.0.0
EXPOSE 80
HEALTHCHECK --interval=1m CMD curl -f http://localhost/ || exit 1