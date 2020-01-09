FROM l3iggs/archlinux
MAINTAINER Patrick Schwartz <p.schwartz92@gmail.com>

RUN pacman -Sy --noconfirm
RUN pacman -S --noconfirm python2-mako deluge unrar unzip

ADD start.sh /start.sh
RUN chmod +x /start.sh

VOLUME ["/data"]
# Torrent port
EXPOSE 53160
EXPOSE 53160/udp
# Daemon
EXPOSE 58846

CMD ["/start.sh"]
