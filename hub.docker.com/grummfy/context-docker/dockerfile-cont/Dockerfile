FROM python:3.7
ENV PYTHONUNBUFFERED 1

# Install node prereqs, nodejs and yarn
# Ref: https://deb.nodesource.com/setup_10.x
# Ref: https://yarnpkg.com/en/docs/install
RUN \
  apt-get update && \
  apt-get install -yqq apt-transport-https libsasl2-dev
RUN \
  echo "deb https://deb.nodesource.com/node_10.x stretch main" > /etc/apt/sources.list.d/nodesource.list && \
  wget -qO- https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - && \
  echo "deb https://dl.yarnpkg.com/debian/ stable main" > /etc/apt/sources.list.d/yarn.list && \
  wget -qO- https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
  apt-get update && \
  apt-get install -yqq nodejs yarn && \
  rm -rf /var/lib/apt/lists/*

# install redis
RUN groupadd -r redis && useradd -r -g redis redis
ENV REDIS_VERSION 5.0.4
ENV REDIS_DOWNLOAD_URL http://download.redis.io/releases/redis-5.0.4.tar.gz
ENV REDIS_DOWNLOAD_SHA 3ce9ceff5a23f60913e1573f6dfcd4aa53b42d4a2789e28fa53ec2bd28c987dd

# for redis-sentinel see: http://redis.io/topics/sentinel
RUN set -ex; \
	wget -O redis.tar.gz "$REDIS_DOWNLOAD_URL"; \
	echo "$REDIS_DOWNLOAD_SHA *redis.tar.gz" | sha256sum -c -; \
	mkdir -p /usr/src/redis; \
	tar -xzf redis.tar.gz -C /usr/src/redis --strip-components=1; \
	rm redis.tar.gz; \
	grep -q '^#define CONFIG_DEFAULT_PROTECTED_MODE 1$' /usr/src/redis/src/server.h; \
	sed -ri 's!^(#define CONFIG_DEFAULT_PROTECTED_MODE) 1$!\1 0!' /usr/src/redis/src/server.h; \
	grep -q '^#define CONFIG_DEFAULT_PROTECTED_MODE 0$' /usr/src/redis/src/server.h; \
	make -C /usr/src/redis -j "$(nproc)"; \
	make -C /usr/src/redis install; \
	rm -r /usr/src/redis;

RUN mkdir /var/redis && chown redis:redis /var/redis

# install memcached
RUN groupadd --system --gid 11211 memcache && useradd --system --gid memcache --uid 11211 memcache
ENV MEMCACHED_VERSION 1.5.14
ENV MEMCACHED_SHA1 94592688ae685caf53ab90a821c99f1503bb1018

RUN set -x \
	&& wget -O memcached.tar.gz "https://memcached.org/files/memcached-$MEMCACHED_VERSION.tar.gz" \
	&& echo "$MEMCACHED_SHA1  memcached.tar.gz" | sha1sum -c - \
	&& mkdir -p /usr/src/memcached \
	&& tar -xzf memcached.tar.gz -C /usr/src/memcached --strip-components=1 \
	&& rm memcached.tar.gz \
	&& cd /usr/src/memcached \
	&& gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
	&& ./configure \
		--build="$gnuArch" \
		--enable-sasl \
	&& make -j "$(nproc)" \
	&& make install \
	&& cd / && rm -rf /usr/src/memcached \
	&& memcached -V

RUN mkdir /var/memcache && chown memcache:memcache /var/memcache

# install nginx
ENV NGINX_VERSION 1.15.12-1~stretch
ENV NJS_VERSION   1.15.12.0.3.1-1~stretch
RUN set -x \
    && \
	NGINX_GPGKEY=573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62; \
	found=''; \
	for server in \
		hkp://keyserver.ubuntu.com:80 \
		hkp://p80.pool.sks-keyservers.net:80 \
		pgp.mit.edu \
	; do \
		echo "Fetching GPG key $NGINX_GPGKEY from $server"; \
		apt-key adv --keyserver "$server" --keyserver-options timeout=10 --recv-keys "$NGINX_GPGKEY" && found=yes && break; \
	done; \
	test -z "$found" && echo >&2 "error: failed to fetch GPG key $NGINX_GPGKEY" && exit 1; \
	apt-get remove --purge --auto-remove -y gnupg1 && rm -rf /var/lib/apt/lists/* \
    && dpkgArch="$(dpkg --print-architecture)" \
	&& nginxPackages=" \
		nginx=${NGINX_VERSION} \
		nginx-module-xslt=${NGINX_VERSION} \
		nginx-module-geoip=${NGINX_VERSION} \
		nginx-module-image-filter=${NGINX_VERSION} \
		nginx-module-njs=${NJS_VERSION} \
	" \
    && echo "deb https://nginx.org/packages/mainline/debian/ stretch nginx" >> /etc/apt/sources.list.d/nginx.list \
	&& apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y \
						$nginxPackages \
						gettext-base \
    && rm -rf /var/lib/apt/lists/* /etc/apt/sources.list.d/nginx.list

# install CustomCRM

RUN mkdir /var/app && chown www-data:www-data /var/app
WORKDIR /var/app
COPY ./requirements.txt /var/app/
RUN pip install -r requirements.txt
COPY . /var/app/

COPY ./nginx.conf /etc/nginx/conf.d/default.conf

VOLUME /var/media
VOLUME /var/site-static
VOLUME /var/app/ui/build
VOLUME /var/app/ui/node_modules
VOLUME /var/logs
VOLUME /var/app/crm/migrations
VOLUME /var/app/extra_apps

RUN chown www-data:www-data /var/media

ENTRYPOINT ["./entrypoint.sh"]
CMD ["run"]