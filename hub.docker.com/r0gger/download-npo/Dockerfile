FROM ubuntu:18.04
RUN apt-get update
RUN apt-get install -y software-properties-common

# install download-npo
RUN add-apt-repository -y ppa:maarten-fonville/download-npo
RUN apt-get update
RUN apt-get -yq install download-npo

RUN mkdir /downloads
WORKDIR /downloads
VOLUME /downloads

# clean up
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
