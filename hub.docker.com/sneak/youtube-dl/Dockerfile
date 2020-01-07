FROM ubuntu:bionic

ENV DEBIAN_FRONTEND noninteractive
ENV HOME /root

RUN apt update && apt -y upgrade
RUN apt install -y python3-pip ffmpeg locales
RUN echo 'en_US.UTF-8 UTF-8' > /etc/locale.gen && locale-gen && update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN pip3 install youtube_dl
ADD youtube-dl.conf /etc/youtube-dl.conf
ADD entrypoint.sh /usr/local/bin/entrypoint.sh

USER nobody:nogroup
WORKDIR /tmp
CMD /bin/bash /usr/local/bin/entrypoint.sh
