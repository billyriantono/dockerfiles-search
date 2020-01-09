FROM pureskillgg/csgo-server:1 as server
RUN rm -rf \
    /home/csgo/hlserver/csgo/csgo/*.vpk \
    /home/csgo/hlserver/csgo/csgo/maps \
    /home/csgo/hlserver/csgo/platform/shaders

FROM ubuntu:18.04

ENV USER csgo
ENV HOME /home/$USER
ENV SERVER $HOME/hlserver

RUN apt-get -y update \
 && apt-get -y upgrade \
 && apt-get -y install lib32gcc1 curl net-tools lib32stdc++6 locales \
 && locale-gen en_US.UTF-8 \
 && update-locale LANG=en_US.UTF-8 LANGUAGE=en_US.UTF-8 LC_ALL=en_US.UTF-8 \
 && dpkg-reconfigure --frontend=noninteractive locales \
 && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN groupadd --gid 1000 $USER \
 && useradd $USER --uid 1000 --gid 1000 --shell /bin/bash \
 && mkdir $HOME \
 && chown $USER:$USER $HOME

ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

COPY --from=server /home/csgo/hlserver /home/csgo/hlserver

RUN chown -R $USER:$USER $SERVER

USER $USER

EXPOSE 27015/udp

WORKDIR $SERVER
