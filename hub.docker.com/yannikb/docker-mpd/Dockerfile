FROM ubuntu:latest
MAINTAINER Yannik Buerkle <mail@yannik-buerkle.de>

RUN apt-get -qq update --fix-missing
RUN locale-gen en_US en_US.UTF-8
RUN dpkg-reconfigure locales

RUN apt-get install -y mpd

ADD mpd.conf /etc/mpd.conf
ADD start.sh /data/mpd/start.sh

RUN mkdir -p /data/mpd/pids
RUN mkdir -p /data/mpd/logs
RUN chown -R mpd /data/mpd
RUN chmod +x /data/mpd/start.sh

EXPOSE 6600 8000

ENTRYPOINT /data/mpd/start.sh
