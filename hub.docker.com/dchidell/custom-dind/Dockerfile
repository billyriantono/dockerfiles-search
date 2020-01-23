FROM docker:18.06.3-dind
MAINTAINER David Chidell (dchidell@cisco.com)

ADD daemon.json /etc/docker/daemon.json
ADD route.sh /usr/local/bin/
RUN chmod a+x /usr/local/bin/route.sh
ENTRYPOINT ["/usr/local/bin/route.sh"]