# VERSION 1.0
# DOCKER-VERSION  1.2.0
# AUTHOR:         Richard Lee <lifuzu@gmail.com>
# DESCRIPTION:    MongoDB Image Container

FROM dockerbase/service

# Run dockerbase script
ADD     mongodb.sh /dockerbase/
RUN     /dockerbase/mongodb.sh

RUN     mkdir -p /etc/service/mongodb
ADD     build/runit/mongodb /etc/service/mongodb/run

VOLUME  ["/data/db"]
