FROM alpine:edge

MAINTAINER Vesyrak

ENV DEBIAN_FRONTEND noninteractive
#RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories

RUN apk add --no-cache \
	alpine-sdk \
        flac-dev \
        alsa-lib-dev \
        faad2-dev \
        mpg123-dev \
        libvorbis-dev \
        libmad-dev \
        && git clone https://github.com/ralph-irving/squeezelite.git 

WORKDIR squeezelite
RUN make && chmod a+x squeezelite \
	&& apk del alpine-sdk

CMD ./squeezelite  

