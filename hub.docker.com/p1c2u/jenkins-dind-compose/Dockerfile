FROM mesosphere/jenkins-dind:0.5.0-alpine

MAINTAINER Artur Maciag <maciag.artur@gmail.com>

RUN curl -L https://github.com/docker/compose/releases/download/1.16.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose

ENTRYPOINT ["dockerd-entrypoint.sh"]
CMD []
