FROM tvaughan/ubuntu:15.10
MAINTAINER "Tom Vaughan <tvaughan@tocino.cl>"

RUN apt-get -q update                   \
    && DEBIAN_FRONTEND=noninteractive   \
    apt-get -q -y install               \
        python3-dev                     \
        python3-pip=*                   \
    && apt-get -q clean                 \
    && rm -rf /var/lib/apt/lists/*

CMD ["python3"]
