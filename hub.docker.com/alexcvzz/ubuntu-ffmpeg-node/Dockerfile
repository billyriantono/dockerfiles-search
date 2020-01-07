FROM ubuntu:16.04

MAINTAINER  Alex Covizzi <alexcovizzi@gmail.com>

## update and install curl and sudo
RUN     apt-get -yqq update && \
        apt-get install -yq --no-install-recommends curl sudo && \
        apt-get autoremove -y && \
        apt-get clean -y

## add jonathonf/ffmpeg ppa
RUN     echo "deb http://ppa.launchpad.net/jonathonf/ffmpeg-3/ubuntu xenial main \n\
              deb-src http://ppa.launchpad.net/jonathonf/ffmpeg-3/ubuntu xenial main" \
        >> /etc/apt/sources.list && \
        apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4AB0F789CBA31744CC7DA76A8CF63AD3F06FC659

## install ffmpeg
RUN     apt-get update && \
        apt-get install -yq ffmpeg

## install nodejs
RUN     curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash - && \
        apt-get install -yq nodejs

## clean
RUN     apt-get autoremove -y && \
        apt-get clean -y


ENTRYPOINT ["/bin/bash"]
