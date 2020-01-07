FROM alpine:3.7
MAINTAINER mikafouenski

RUN apk add --no-cache python ffmpeg && \
    wget https://yt-dl.org/downloads/latest/youtube-dl -O /usr/local/bin/youtube-dl && \
    chmod +rx /usr/local/bin/youtube-dl

ENTRYPOINT ["youtube-dl"]
