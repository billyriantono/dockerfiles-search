FROM centos:7
MAINTAINER "Jeff Geiger" <@jeffgeiger>

USER root
RUN yum clean all && rm -rf /var/cache/yum && yum makecache && \
 yum install epel-release -y && \
 yum makecache fast && \
 yum install which python-pip python-devel gcc make python-xlib python-pillow-tk libX11-devel openssl-devel git tcpdump tmux -y && \
 cd /opt/ && \
 git clone https://github.com/n1nj4sec/pupy.git pupy && \
 cd pupy && \
 git submodule init && \
 git submodule update && \
 pip install python-xlib && \
 curl -O http://mirror.centos.org/centos/7/os/x86_64/Packages/xorg-x11-server-Xvfb-1.19.3-11.el7.x86_64.rpm && \
 yum install xorg-x11-server-Xvfb-1.19.3-11.el7.x86_64.rpm -y && \
 xvfb-run pip install -r pupy/requirements.txt && \
 curl -LO https://github.com/n1nj4sec/pupy/releases/download/latest/payload_templates.txz && \
 tar xvf payload_templates.txz && mv -f payload_templates/* pupy/payload_templates/ && rm -f payload_templates.txz && rm -rf payload_templates && \
 mkdir /tmp/loot

WORKDIR /opt/pupy

ENTRYPOINT /bin/bash

