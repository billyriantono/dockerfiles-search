FROM nginx:alpine

LABEL maintainer="docker-dario@neomediatech.it"

EXPOSE 80/tcp 443/tcp
COPY conf/rspamd-reverse.conf etc/nginx/conf.d/

# psutils net-tools
RUN apk update; apk upgrade ; apk add --no-cache tzdata; cp /usr/share/zoneinfo/Europe/Rome /etc/localtime
RUN rm -rf /usr/local/share/doc /usr/local/share/man
RUN rm /etc/nginx/conf.d/default.conf
