FROM ubuntu:latest

ENV LANG C.UTF-8

ADD install.sh /tmp/install.sh
RUN sh /tmp/install.sh

ADD install_docker.sh /tmp/install_docker.sh
RUN sh /tmp/install_docker.sh

ADD install_heroku.sh /tmp/install_heroku.sh
RUN sh /tmp/install_heroku.sh
