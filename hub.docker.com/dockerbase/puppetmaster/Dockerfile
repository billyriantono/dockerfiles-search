# VERSION 1.0
# DOCKER-VERSION  1.2.0
# AUTHOR:         Richard Lee <lifuzu@gmail.com>
# DESCRIPTION:    Puppetmaster Image Container

FROM dockerbase/service

# Run dockerbase script
ADD     puppetmaster.sh /dockerbase/
RUN     /dockerbase/puppetmaster.sh

RUN     mkdir -p /etc/service/puppetmaster
ADD     build/runit/puppetmaster /etc/service/puppetmaster/run

EXPOSE 8140
