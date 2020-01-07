FROM alpine:latest
ENV EDGE_REPOSITORY=http://dl-cdn.alpinelinux.org/alpine/edge/main
RUN apk update --repository $EDGE_REPOSITORY \
    && apk --no-cache add ca-certificates \
    && apk add py-pip \
    && apk add ffmpeg --repository $EDGE_REPOSITORY
RUN pip install --upgrade pip
RUN pip install --upgrade setuptools
RUN pip install -I flexget transmissionrpc
RUN pip install -I youtube-dl
RUN mkdir /flexget
WORKDIR /flexget	
CMD ["/usr/local/bin/flexget", "--loglevel", "info", "daemon", "start"]
