FROM ubuntu:17.04
MAINTAINER skaronator

ENV DEBIAN_FRONTEND noninteractive
ENV HOME /
ENV THREADS 4
ENV RUN_EVERY_SEC 600

VOLUME ["/config"]
VOLUME ["/output"]
VOLUME ["/world"]

RUN apt-get update && \
    apt-get -y install python curl wget apt-transport-https cron imagemagick&& \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN echo "deb https://packages.mapcrafter.org/ubuntu zesty main" | tee "/etc/apt/sources.list.d/mapcrafter.list" && \
    wget -O "/etc/apt/trusted.gpg.d/mapcrafter.gpg" "https://packages.mapcrafter.org/ubuntu/keyring.gpg"

RUN apt-get update && \
    apt-get -y install mapcrafter && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD render.sh /
RUN chmod 0777 /render.sh
ADD render.conf /

CMD /render.sh´
