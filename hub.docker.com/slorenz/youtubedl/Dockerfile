FROM alpine

RUN apk --update add youtube-dl
RUN mkdir /mp3

WORKDIR /mp3

ENTRYPOINT ["/usr/bin/youtube-dl"]