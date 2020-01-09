#-- copyright
# OpenProject-docker is a set-up script for OpenProject using the
# 'Apache 2.0' licensed docker container engine. See
# http://docker.io and https://github.com/dotcloud/docker for details
#
# OpenProject is a project management system.
# Copyright (C) 2013 the OpenProject Foundation (OPF)
#
# This program is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public License
# version 3.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301, USA.
#
# See COPYRIGHT.md for more details.
#++

FROM centos:6.6

MAINTAINER DRIVEUP Developers, driveup.developers@gmail.com

RUN rpm --import https://rpm.packager.io/key

ADD ./pkgr-openproject-community.repo /etc/yum.repos.d/pkgr-openproject-community.repo

RUN yum --setopt=tsflags=nodocs -y install \
    memcached \
    mysql-server \
    mysql-client \
    python-setuptools \
    openproject-ce \
    && rm -rf /var/cache/yum/* \
    && yum clean all

RUN easy_install supervisor

ENV DATABASE_URL=mysql2://root:p4s5w0rd@127.0.0.1:3306/openproject
ENV SECRET_TOKEN=c5aa99a90f9650404a900cf5ec7c28f7fe1379550bb811cb0b39058f9400eaa216b9b2b22d27f58fb15ac21adb3bd16494ebe89e39ec225ef4627db048a12530
ENV ADMIN_EMAIL=admin@yourcompany.com
ENV EMAIL_DELIVERY_METHOD=smtp
ENV SMTP_DOMAIN=smtp.gmail.com
ENV SMTP_HOST=smtp.gmail.com
ENV SMTP_PASSWORD=yourpassword
ENV SMTP_PORT=587
ENV SMTP_USERNAME=yourusername
ENV SMTP_URL=smtp://$SMTP_USERNAME:$SMTP_PORT@$SMTP_HOST:$SMTP_PORT/$SMTP_DOMAIN

ADD ./mysqlStartup.sh /opt/openproject-ce/mysqlStartup.sh
RUN /bin/bash /opt/openproject-ce/mysqlStartup.sh

RUN /usr/bin/openproject-ce config:set DATABASE_URL=${DATABASE_URL} \
    && /usr/bin/openproject-ce config:set SECRET_TOKEN=${SECRET_TOKEN} \
    && /usr/bin/openproject-ce config:set ADMIN_EMAIL=${ADMIN_EMAIL} \
    && /usr/bin/openproject-ce config:set EMAIL_DELIVERY_METHOD=${EMAIL_DELIVERY_METHOD} \
    && /usr/bin/openproject-ce config:set SMTP_DOMAIN=${SMTP_DOMAIN} \
    && /usr/bin/openproject-ce config:set SMTP_HOST=${SMTP_HOST} \
    && /usr/bin/openproject-ce config:set SMTP_PASSWORD=${SMTP_PASSWORD} \
    && /usr/bin/openproject-ce config:set SMTP_PORT=${SMTP_PORT} \
    && /usr/bin/openproject-ce config:set SMTP_USERNAME=${SMTP_USERNAME} \
    && /usr/bin/openproject-ce config:set SMTP_URL=smtp://${SMTP_USERNAME}:${SMTP_PORT}@${SMTP_HOST}:${SMTP_PORT}/${SMTP_DOMAIN}

ADD ./openprojectStartup.sh /opt/openproject-ce/openprojectStartup.sh
RUN /bin/bash /opt/openproject-ce/openprojectStartup.sh

ADD ./supervisord/ /etc/supervisord/

EXPOSE 3000

CMD /usr/bin/supervisord --configuration=/etc/supervisord/supervisord.conf
