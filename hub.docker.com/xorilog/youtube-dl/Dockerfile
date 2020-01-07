FROM alpine:3.6
# How to use
# docker run --rm -ti \
#   -v /tmp/video:/tmp/video \
#   xorilog/youtube-dl <video url>
#
# For youtube-dl doc see : https://github.com/rg3/youtube-dl/blob/master/README.md#readme 
RUN apk add --update curl python3 python \
    && curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl \
    && chmod a+rx /usr/local/bin/youtube-dl
WORKDIR /tmp/video
ENTRYPOINT ["youtube-dl"]
