#
# To build this Docker image: docker build -t fpm .
#
# To run this Docker container interactively: docker run -it fpm
#
FROM alpine:latest

RUN apk add --no-cache \
        ruby \
        ruby-dev \
        ruby-etc \
        gcc \
        libffi-dev \
        make \
        libc-dev \
        rpm \
        tar \
    && gem install --no-ri --no-rdoc fpm

ENTRYPOINT ["fpm"]
