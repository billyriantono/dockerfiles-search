FROM cloudaku/ubuntu-base
MAINTAINER Cloudaku <devops@hostname.io>

RUN cd /tmp && \
    wget http://downloads.drone.io/latest/drone.deb && \
    dpkg -i drone.deb

EXPOSE 8080
CMD ["droned"]
