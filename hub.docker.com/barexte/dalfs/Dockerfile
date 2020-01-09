FROM alpine:3.8

MAINTAINER BAREXTE <barexte@gmail.com>

# Install nginx
RUN apk add --update --no-cache nginx
RUN mkdir -p /run/nginx

# Install shadow
RUN apk add --update --no-cache shadow

# Copy default configuration
RUN rm /etc/nginx/conf.d/default.conf
COPY conf.d/ /etc/nginx/conf.d/

# Copy defult page
RUN mkdir -p /usr/share/nginx/html
COPY html/ /usr/share/nginx/html/

# create mountpoint 'date'
RUN mkdir -p /data

# Copy start script
COPY ./start.sh /sbin/
RUN chmod +x /sbin/start.sh

EXPOSE 80
VOLUME /data

ENTRYPOINT ["start.sh"]
