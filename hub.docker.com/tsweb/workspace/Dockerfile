FROM tsweb/terminal
MAINTAINER Kazuhisa Kumagai <k-kumagai@ts.tv-osaka.co.jp>

#--------------------------------------
# install lab-command
#--------------------------------------

RUN npm install -g lab-command --unsafe-perm=true --allow-root

#--------------------------------------
# run
#--------------------------------------

ADD start.sh /start.sh
RUN chmod +x /start.sh

CMD ["/start.sh"]
