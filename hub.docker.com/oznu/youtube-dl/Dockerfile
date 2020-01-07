FROM alpine:latest

RUN apk add --no-cache curl python ffmpeg \
  && curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl \
  && chmod a+rx /usr/local/bin/youtube-dl \
  && mkdir /out

WORKDIR /out

ENTRYPOINT ["youtube-dl"]
