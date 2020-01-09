FROM ubuntu:precise
RUN echo deb http://archive.ubuntu.com/ubuntu/ precise main universe > /etc/apt/sources.list.d/precise.list
RUN apt-get update -q
RUN apt-get install -qy pptpd iptables
ADD ./bin /usr/local/sbin
VOLUME /etc/ppp
EXPOSE 1723/tcp
CMD run