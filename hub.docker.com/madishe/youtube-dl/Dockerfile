#
# Dockerfile for youtube-dl
#

FROM alpine:latest
#MAINTAINER madishe <madishe@gmail.com>

#Need to update alpine first
RUN apk update
RUN apk upgrade

#Install required stuff
RUN set -xe \
    && apk add --no-cache ca-certificates \
                          ffmpeg \
                          openssl \
                          python3 \
    && pip3 install --upgrade pip \
    && pip3 install youtube-dl

#need to create a special catalog, by default it is /data
#alias yt='docker run --rm -u $(id -u):$(id -g) -v $PWD:/data madishe/youtube-dl'
WORKDIR /tmp/data/youtube-dl

ENTRYPOINT ["youtube-dl"]
CMD ["--help"]
