FROM ubuntu:latest
MAINTAINER zhiyi liu <liuzhiyi@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
#Only for Chinese user
RUN apt-get -qq update && \
    apt-get -qqy install --no-install-recommends \
       gdbserver &&\
     rm -rf /var/lib/apt/lists/* &&\
     mkdir -p /root/build

EXPOSE 10234/tcp
EXPOSE 10234/udp

CMD [ "sh", "-c", "gdbserver 127.0.0.1:10234 $EXEC" ]

