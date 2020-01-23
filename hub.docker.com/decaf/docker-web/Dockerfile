FROM nginx

ADD nginx.conf /etc/nginx/conf.d/default.conf

RUN apt-get update --fix-missing && \
	apt-get install -y \
    vim

RUN adduser -D -H -u 33 -s /bin/bash www-data

RUN mkdir -p /var/www/html/public

ENV HISTCONTROL="ignoredups"
