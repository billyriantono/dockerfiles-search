# VERSION 1.2
# DOCKER-VERSION  1.2.0
# AUTHOR:         Richard Lee <lifuzu@gmail.com>
# DESCRIPTION:    Docker Image Container

FROM dockerbase/devbase

USER    root
# Run dockerbase script
ADD     docker.sh /dockerbase/
RUN     /dockerbase/docker.sh

# Add docker into runit
ADD     build/runit/docker /etc/service/docker/run

