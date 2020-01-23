FROM neurodebian:xenial
MAINTAINER Soichi Hayashis <hayashis@iu.edu>

# Install LXDE, VNC server, XRDP
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
   xvfb x11vnc vim lxde-core lxde-icon-theme lxterminal

EXPOSE 5900

#install mricron
RUN apt-get install -y mricron

RUN mkdir -p /root/.config/autostart

ADD vnc.sh /opt
ADD start.sh /
ADD start.desktop /root/.config/autostart

CMD ["/opt/vnc.sh"]
