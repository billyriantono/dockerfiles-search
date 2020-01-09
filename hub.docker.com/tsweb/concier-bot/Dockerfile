FROM tsweb/hubot-idobata
MAINTAINER Kazuhisa Kumagai <k-kumagai@ts.tv-osaka.co.jp>

#--------------------------------------
# install Hubot-idobata-temtem
#--------------------------------------

RUN cd /root/hubot &&\
	npm install cron --save &&\
	npm install

#--------------------------------------
# initialize
#--------------------------------------

ADD supervisor.conf /etc/supervisord/conf/service.conf
CMD ["/usr/bin/supervisord"]
