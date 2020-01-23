FROM ubuntu:latest
RUN apt-get -y update && apt-get -y install qbittorrent-nox
RUN mkdir /root/Download

EXPOSE 8080/tcp 8999/tcp 8999/udp

CMD ["/usr/bin/qbittorrent-nox"]

