FROM tsweb/node:12
MAINTAINER Kazuhisa Kumagai <k-kumagai@ts.tv-osaka.co.jp>

#--------------------------------------
# initialize
#--------------------------------------

ADD supervisor.conf /etc/supervisord/conf/service.conf

#--------------------------------------
# install labot
#--------------------------------------

RUN npm install -g labot --unsafe-perm=true --allow-root

#--------------------------------------
# run
#--------------------------------------

ADD start.sh /start.sh
RUN chmod +x /start.sh

CMD ["/start.sh"]
