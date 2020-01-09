FROM ubuntu:18.04

ARG SHELL=$SHELL
ARG DOCKER_USER=$DOCKER_USER
ARG DOCKER_GROUP=$DOCKER_GROUP

ENV SHELL $SHELL

COPY setup.sh /opt/setup.sh
RUN /bin/bash /opt/setup.sh

USER $DOCKER_USER

CMD tail -f /dev/null
