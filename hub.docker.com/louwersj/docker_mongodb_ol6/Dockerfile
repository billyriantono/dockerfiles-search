# NAME:
#   Dockerfile
#
# DESC:
#   Dockerfile for building a Docker container which contains the
#   MongoDB database. This container will be based upon the Oracle
#   Linux container. Port 27017 will be opend to enable connections
#   to the container. 
#
# LOG:
# VERSION---DATE--------NAME-------------COMMENT
# 0.1       14JUL17     Johan Louwers    Initial upload to github.com
#
# LICENSE:
# Copyright (C) 2015  Johan Louwers
#
# This code is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public License
# as published by the Free Software Foundation; either version 2
# of the License, or (at your option) any later version.
#
# This code is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this code; if not, write to the Free Software
# Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  
# 02110-1301, USA.
# *
# */

FROM oraclelinux:6.9
MAINTAINER Johan Louwers <louwersj@gmail.com>
LABEL maintainer="louwersj@gmail.com"

# Parse arguments for the build command.
ARG VERSION
ARG VCS_URL
ARG VCS_REF
ARG BUILD_DATE

# A little bit of metadata management.
# See http://label-schema.org/
LABEL org.label-schema.schema-version="1.0" \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vendor="louwersj@gmail.com" \
      org.label-schema.version=$VERSION \
      org.label-schema.vcs-url=$VCS_URL \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.name="MongoDB" \
      org.label-schema.description="MongoDB 3.4 for Oracle Linux 6"

# Ensure we have wget, which we will use in a second
# step to download some configuration files
RUN yum -y install wget ; yum clean all

# Download the YUM repository file to ensure we can use 
# the MongoDB repository to install MongoDB. We use the 
# .repo file as it stored on the github repository for
# this Dockerfile
RUN wget https://raw.githubusercontent.com/louwersj/docker_mongodb_ol6/master/mongodb_3.4/OL6.9/mongodb-org-3.4.repo -O /etc/yum.repos.d/mongodb-org-3.4.repo

# install MongoDB with yum and clean yum
RUN yum -y install mongodb-org-server ; yum clean all

# Create the data directory to enable MongoDB to store 
# database itself
RUN mkdir -p /data/db

EXPOSE 27017
ENTRYPOINT ["/usr/bin/mongod"]
