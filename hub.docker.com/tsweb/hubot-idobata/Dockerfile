FROM tsweb/hubot
MAINTAINER Kazuhisa Kumagai <k-kumagai@ts.tv-osaka.co.jp>

#--------------------------------------
# install Hubot-idobata
#--------------------------------------

RUN cd /root/hubot &&\
	npm install hubot-idobata querystring --save &&\
	npm install

ADD scripts /root/hubot/scripts

# ENV
ENV HUBOT_NAME hubot
ENV PORT 8080
ENV HUBOT_IDOBATA_API_TOKEN XXXXXXXXXXXXXXXXXXXXXXXXX
ENV HUBOT_IDOBATA_ROOM_ID XXXX

#--------------------------------------
# initialize
#--------------------------------------

ADD supervisor.conf /etc/supervisord/conf/service.conf
CMD ["/usr/bin/supervisord"]
