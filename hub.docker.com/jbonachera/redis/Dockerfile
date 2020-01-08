FROM jbonachera/arch
MAINTAINER Julien BONACHERA <julien@bonachera.fr>
EXPOSE 6379
CMD ["/usr/bin/redis-server", "/etc/redis.conf", "--daemonize no"]
RUN pacman -S --noconfirm redis
USER redis
VOLUME /var/lib/redis/
COPY redis.conf /etc/redis.conf
