FROM resin/raspberry-pi-alpine:3.6

ENV NGINX_VERSION 1.12.2-r1
ENV CERTBOT_VERSION 0.14.0-r0
ENV APACHE2_UTILS_VERSION 2.4.33-r0

RUN ["cross-build-start"]

RUN apk add --no-cache nginx=${NGINX_VERSION} \
		certbot=${CERTBOT_VERSION} \
		apache2-utils=${APACHE2_UTILS_VERSION} \
	&& mkdir -p /run/nginx \
	&& mkdir -p /var/www/certbot \
	&& ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log

COPY certbot-renew /etc/periodic/daily/certbot-renew

RUN chmod +x /etc/periodic/daily/certbot-renew

RUN ["cross-build-end"]

VOLUME ["/etc/nginx", "/etc/letsencrypt"]

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"] 
