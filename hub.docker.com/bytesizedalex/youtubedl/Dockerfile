FROM alpine:latest
MAINTAINER Alex Bytes bytesizedalex@users.noreply.github.com
LABEL Name=youtube-dl Version=1.0.1 
RUN apk add youtube-dl --no-cache && rm -f /var/cache/apk/*
ENTRYPOINT ["youtube-dl"]
