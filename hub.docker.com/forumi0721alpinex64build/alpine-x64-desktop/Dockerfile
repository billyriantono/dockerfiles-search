FROM forumi0721alpinex64/alpine-x64-dev:latest

LABEL maintainer="forumi0721@gmail.com"

COPY local/. /usr/local/

#RUN ["docker-build-start"]

RUN ["docker-init"]

#RUN ["docker-build-end"]

ENTRYPOINT ["docker-run"]

