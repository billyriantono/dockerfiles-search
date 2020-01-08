FROM		redis:5.0.2-stretch

RUN apt-get update &&\
    apt-get -y upgrade &&\
    apt-get install -y supervisor git libluajit-5.1-dev liblua5.1-dev libevent-dev gcc make &&\
    apt-get clean &&\
    rm -rf /var/lib/apt/lists/* &&\
    git clone git://github.com/nicolasff/webdis.git /usr/local/src/webdis/

#compile and install webdis
WORKDIR		/usr/local/src/webdis/

RUN		make && make install && \
      groupadd -r webdis && \
      useradd -r -g webdis webdis

ADD 	src/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD		src/redis.conf src/redis-rename-command.conf src/webdis.conf /etc/
ADD		src/webdis-delay.sh /usr/local/bin/webdis-delay.sh

RUN   touch /var/log/redis.log && \
      rm /etc/webdis.prod.json && \
      chmod +x /usr/local/bin/webdis-delay.sh && \
      chown webdis: /etc/webdis.conf  && \
      chown redis: /var/log/redis.log /etc/redis.conf /etc/redis-rename-command.conf && \
      chmod 444 /etc/redis.conf /etc/redis-rename-command.conf /etc/webdis.conf && \
      mkdir /var/run/supervisord

RUN apt-get remove -y git gcc make &&\
    apt-get -y autoremove

VOLUME /var/log/
USER root

EXPOSE		6379
EXPOSE		7379

ENTRYPOINT	["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
