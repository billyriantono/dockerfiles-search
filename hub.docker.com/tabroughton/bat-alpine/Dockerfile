FROM alpine:edge

MAINTAINER Tom Broughton <docker@tombroughton.me>

WORKDIR /myapp

RUN \
    echo http://nl.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories 

RUN \
    apk --update add bash bat git less  && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

# configure bash to check window size after each command
RUN \
    echo "shopt -s checkwinsize" >> ~/.bashrc


# execute `bat` after a slight pause in order to give
# the tty time to realize the current window size
ENTRYPOINT [ "bash", "-c", "sleep 0.1; bat $0 $@" ]
