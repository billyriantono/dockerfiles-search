FROM ubuntu:latest as builder

WORKDIR /dependencies
COPY gcc-arm-none-eabi-7-2018-q2-update-linux.tar.bz2 .

WORKDIR /home/dev
RUN tar xf /dependencies/gcc-arm-none-eabi-7-2018-q2-update-linux.tar.bz2
RUN rm -rf gcc-arm-none-eabi-7-2018-q2-update/share/doc

FROM frolvlad/alpine-glibc:latest
RUN apk add --no-cache \
    python \
    scons \
    && apk update

COPY --from=builder /home/dev/ /home/dev/
ENV PATH="/home/dev/gcc-arm-none-eabi-7-2018-q2-update/bin:${PATH}"

WORKDIR /usr/project
