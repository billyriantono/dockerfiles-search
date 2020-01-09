FROM centos:7

LABEL maintainer "tester"

ENV NB_USER="tester"

RUN echo "now testing"

COPY mytest/hello.txt /home/$NB_USER/

CMD cat /home/$NB_USER/hello.txt