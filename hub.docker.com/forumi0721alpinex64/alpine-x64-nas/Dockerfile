FROM forumi0721/alpine-x64-base:latest

LABEL maintainer="forumi0721@gmail.com"

COPY local/. /usr/local/

#RUN ["docker-build-start"]

RUN ["docker-init"]

#RUN ["docker-build-end"]

ENTRYPOINT ["docker-run"]

EXPOSE 22/tcp 137/udp 138/udp 139/tcp 445/tcp 8200/tcp 9091/tcp 51413/tcp 51413/udp 8080/tcp

VOLUME /conf.d /data

