FROM ubuntu:16.04
MAINTAINER andyzhshg <andyzhshg@gmail.com>

RUN apt-get update && apt-get install -y libc6-i386 lib32z1

WORKDIR /xware
ADD Xware_x86_32_glibc.tar.gz /xware
ADD monitor.sh /xware

VOLUME /data

CMD ["./monitor.sh"]
