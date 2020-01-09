FROM mini/base:latest
MAINTAINER Br4zzor <br4zzor@protonmail.com>

RUN apk --update add nmap && rm -f /var/cache/apk/*

RUN mkdir /work-session
VOLUME ["/work-session"]
WORKDIR /work-session

ENTRYPOINT ["nmap"]
