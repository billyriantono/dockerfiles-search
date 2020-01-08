FROM asdlfkj31h/debian-novnc:0.2
MAINTAINER Gerolf Ziegenhain <gerolf.ziegenhain@gmail.com>

USER 0

RUN apt-get -y install calibre

# set user to 1000 - further installations with user 0
#USER 1000

# Startup
ENTRYPOINT ["/dockerstartup/vnc_startup.sh"]
CMD ["/usr/bin/calibre"]
