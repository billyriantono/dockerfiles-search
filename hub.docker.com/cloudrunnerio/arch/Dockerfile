FROM base/arch

MAINTAINER CloudRunner.IO Dev, dev@cloudrunner.io

RUN pacman-key --refresh-keys
RUN pacman-key --populate archlinux

RUN pacman -Syu --noconfirm
RUN pacman-db-upgrade
RUN pacman -Sy --noconfirm python2 python2-pip python2-m2crypto gcc

RUN mkdir -p /etc/cloudrunner
RUN mkdir -p /opt/cloudrunner
RUN mkdir -p /var/run/sock/cloudrunner/
RUN mkdir -p /var/lib/cloudrunner/

RUN pip2 install cloudrunner

RUN cloudrunner-node configure --server 0.0.0.0

RUN cloudrunner-node details

ADD startup /opt/startup
ADD cloudrunner-node.conf /etc/cloudrunner/cloudrunner-node.conf

ENTRYPOINT ["/opt/startup"]

