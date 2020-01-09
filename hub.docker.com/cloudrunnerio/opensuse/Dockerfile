FROM opensuse:bottle

MAINTAINER CloudRunner.IO Dev, dev@cloudrunner.io

RUN zypper -n --gpg-auto-import-keys up
RUN zypper -n in gcc-c++ python-devel python-pip python-m2crypto python-psutil

RUN mkdir -p /etc/cloudrunner
RUN mkdir -p /opt/cloudrunner
RUN mkdir -p /var/run/sock/cloudrunner/
RUN mkdir -p /var/lib/cloudrunner/

RUN pip install cloudrunner

RUN cloudrunner-node configure --server 0.0.0.0

RUN cloudrunner-node details

ADD startup /opt/startup
ADD cloudrunner-node.conf /etc/cloudrunner/cloudrunner-node.conf

ENTRYPOINT ["/opt/startup"]
