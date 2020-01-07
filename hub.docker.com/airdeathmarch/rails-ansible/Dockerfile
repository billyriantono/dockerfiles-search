FROM ruby:2.2.3

MAINTAINER urasin <urasin2012@gmail.com>

ADD http://dev.mysql.com/get/mysql-apt-config_0.1.5-2ubuntu14.04_all.deb /tmp/
RUN DEBIAN_FRONTEND=noninteractive dpkg -i /tmp/mysql-apt-config_0.1.5-2ubuntu14.04_all.deb
RUN DEBIAN_FRONTEND=noninteractive apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install mysql-server

RUN apt-get -y update && \
    apt-get install -y python-yaml python-jinja2 python-httplib2 python-keyczar python-paramiko python-setuptools python-pkg-resources git python-pip nodejs
RUN pip install ansible
ENTRYPOINT /etc/init.d/mysql start && /bin/bash
