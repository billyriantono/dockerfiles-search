FROM viktor117/php7-fpm:latest
MAINTAINER Viktor Tverdun <v.tverdun@gmail.com>

RUN apt-get update && apt-get install -y supervisor
RUN mkdir -p /var/log/supervisor

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
