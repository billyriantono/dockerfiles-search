FROM alpine:3.4

MAINTAINER Tobias Maxham <git2018@maxham.de>

RUN apk add --no-cache curl ffmpeg python python-dev py-pip \
        && pip install --upgrade pip youtube-dl \
        && mkdir -p /downloads

WORKDIR /downloads

VOLUME ["/downloads"]

ENTRYPOINT ["youtube-dl"]
CMD ["--help"]
