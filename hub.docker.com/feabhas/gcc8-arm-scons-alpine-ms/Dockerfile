FROM ubuntu:latest as builder

WORKDIR /dependencies
COPY gcc-arm-none-eabi-8-2018-q4-major-linux.tar.bz2 .

WORKDIR /home/dev
RUN tar xf /dependencies/gcc-arm-none-eabi-8-2018-q4-major-linux.tar.bz2
RUN rm -rf gcc-arm-none-eabi-8-2018-q4-major/share/doc

FROM frolvlad/alpine-glibc:latest
RUN apk add --no-cache \
    python \
    scons \
    && apk update

COPY --from=builder /home/dev/ /home/dev/
ENV PATH="/home/dev/gcc-arm-none-eabi-8-2018-q4-major/bin:${PATH}"

WORKDIR /usr/project
