FROM ubuntu:16.04

RUN \
    apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository -y ppa:flexiondotorg/audio && \
    apt-get update

RUN apt-get install -y mp3gain

WORKDIR /files

VOLUME [ "/files" ]

CMD mp3gain -c -r *.mp3
