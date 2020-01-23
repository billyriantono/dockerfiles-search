FROM debian:stretch
MAINTAINER François Billant <fbillant@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV VERSION=v1.5.0

copy entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

RUN sed -i.bak 's/stretch main/stretch main contrib non-free/g' /etc/apt/sources.list && \
apt-get update && \
apt-get install -y \
git \
python3 \
python3-libvirt \
libosinfo-1.0-dev \
gobject-introspection \
libglib2.0-bin \
intltool \
python3-gi \
libvirt-glib-1.0-dev \
python3-libxml2 \
python3-requests \
libgtk-3-dev \
gir1.2-vte-2.91 \
gir1.2-gtk-vnc-2.0 \
gir1.2-spice-client-gtk-3.0 \
python3-gi-cairo \
ssh-askpass-gnome \
--no-install-recommends \
&& rm -rf /var/lib/apt/lists/*

RUN cd /opt && \
git clone https://github.com/virt-manager/virt-manager.git && \
cd virt-manager && \
#TODO: Currently broken because setup.py at tag 1.5.0 is for python2... Workaround, build from master...
#git checkout tags/$VERSION && \
./setup.py install && \
cd /opt && \
rm -Rf /opt/virt-manager

entrypoint ["/entrypoint.sh"]
