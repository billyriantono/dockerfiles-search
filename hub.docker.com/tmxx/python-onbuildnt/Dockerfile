FROM ubuntu

RUN apt-get update
RUN apt-get install -y rtorrent 

EXPOSE 52257
EXPOSE 29382
EXPOSE 29382/udp
VOLUME /downloads
VOLUME /rtorrent-config
ENV TERM xterm

CMD rtorrent -n -o  import=/rtorrent-config/rtorrent.rc
