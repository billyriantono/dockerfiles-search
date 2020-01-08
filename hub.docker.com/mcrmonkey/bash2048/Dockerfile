FROM alpine:latest
LABEL MAINTAINER "ant <git@manchestermonkey.co.uk>"

RUN apk --no-cache add git bash bc && adduser -D 2oh48

USER 2oh48

WORKDIR /home/2oh48

RUN git clone https://github.com/mydzor/bash2048.git

ENTRYPOINT ./bash2048/bash2048.sh
