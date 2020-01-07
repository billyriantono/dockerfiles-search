FROM nginx:stable-alpine
RUN \
apk add --no-cache curl ca-certificates openssl socat bash git && \
mkdir -p /root/acme.config
ENV LE_CONFIG_HOME "/root/acme.config"
RUN \
wget -O -  https://get.acme.sh | sh && \
ln -s /root/.acme.sh/acme.sh /usr/local/bin/acme.sh


RUN set +x; \
	addgroup -g 82 -S www-data; \
	adduser -u 82 -D -S -G www-data www-data
