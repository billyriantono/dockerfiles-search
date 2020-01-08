FROM orukami/fpm-nginx:7.0

ENV WORDPRESS_VERSION 4.4.1
ENV WORDPRESS_SHA1 89bcc67a33aecb691e879c818d7e2299701f30e7

# replace origin entrypoint
COPY entrypoint.sh /entrypoint.sh

RUN curl -o wordpress.tar.gz -SL https://wordpress.org/wordpress-${WORDPRESS_VERSION}.tar.gz && \
	echo "$WORDPRESS_SHA1 *wordpress.tar.gz" | sha1sum -c - && \
	tar -xzf wordpress.tar.gz -C ${WWW_ROOT} && rm wordpress.tar.gz && \
	mv ${WWW_ROOT}/wordpress ${PUBLIC_ROOT} && \
	chown -R www-data:www-data ${WWW_ROOT} && \
	chmod +x /entrypoint.sh

WORKDIR ${PUBLIC_ROOT}