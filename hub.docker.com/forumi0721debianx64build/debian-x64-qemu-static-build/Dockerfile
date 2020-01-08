ARG BUILD_ARCH=x64

FROM forumi0721/debian-${BUILD_ARCH}-base:latest as builder

LABEL maintainer="forumi0721@gmail.com"

COPY local/. /usr/local/

#RUN ["docker-build-start"]

RUN ["docker-init"]

#RUN ["docker-build-end"]



FROM forumi0721/debian-x64-base:latest

LABEL maintainer="forumi0721@gmail.com"

COPY --from=builder /opt /opt

COPY local/. /usr/local/

#RUN ["docker-build-start"]

#RUN ["docker-init"]

#RUN ["docker-build-end"]

