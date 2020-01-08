FROM wd29/base
MAINTAINER Benjamin Favre <ben@webdesign29.net>

RUN rm -Rf /etc/nginx/conf.d/* && \
    rm -Rf /etc/nginx/sites-available/* && \
    rm -Rf /var/www/*

ADD ./etc/ /etc/
ADD ./var/ /var/

CMD ["supervisord", "--configuration", "/etc/supervisor/conf.d/supervisor.conf"]