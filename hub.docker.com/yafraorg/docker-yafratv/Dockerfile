#
#  Copyright 2015 yafra.org
#
#  Licensed under the Apache License, Version 2.0 (the "License");
#  you may not use this file except in compliance with the License.
#  You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
#  Unless required by applicable law or agreed to in writing, software
#  distributed under the License is distributed on an "AS IS" BASIS,
#  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#  See the License for the specific language governing permissions and
#  limitations under the License.

#
# yafra.org sagetv run time docker with HD Homerun support
#


# source is yafra ubuntu
FROM ubuntu:14.04.4

MAINTAINER Martin Weber <info@yafra.org>

ENV DEBIAN_FRONTEND noninteractive
ENV JAVA_ARCH="amd64"
ENV JDK_HOME="/usr/lib/jvm/java-7-openjdk-$JAVA_ARCH/"
ENV SAGETV_REPO="https://github.com/google/sagetv.git"

# Speed up APT
RUN echo "force-unsafe-io" > /etc/dpkg/dpkg.cfg.d/02apt-speedup \
  && echo "Acquire::http {No-Cache=True;};" > /etc/apt/apt.conf.d/no-cache

# Install dependencies
RUN set -x && apt-get update \
    && apt-get install -y unzip \
        build-essential \
        git wget ftp \
        libx11-dev libxt-dev libraw1394-dev libavc1394-dev libiec61883-dev \
        libfreetype6-dev yasm autoconf libtool openjdk-7-jdk \
        libaudio-dev libpulse-dev libasound-dev

RUN rm -rf /var/lib/apt/lists/*

WORKDIR /work

#RUN mkdir -p /opt/sagetv && \
#  cd /opt/sagetv && \
#  wget https://bintray.com/artifact/download/yafraorg/yafra-distribution/sagetv-server_9.0.3_amd64.tar.gz && \
#  tar xvfz sagetv-server_9.0.3_amd64.tar.gz && \
#  rm sagetv-server_9.0.3_amd64.tar.gz

RUN cd /work && \
  git clone https://github.com/google/sagetv.git && \
  cd sagetv/build && \
  ./buildall.sh

RUN cd /work && \
  cd sagetv/build && \
  dpkg -i sagetv-server_9.0.4_amd64.deb && \
  service sagetv restart

RUN cd /work && \
  wget http://download.silicondust.com/hdhomerun/libhdhomerun_20150826.tgz && \
  tar xvfz libhdhomerun*tgz

RUN cd /work && \
  git clone https://github.com/yafraorg/xmltvplugin

COPY run-docker.sh /work/run-docker.sh
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
RUN cd /work && \
  chmod 755 run-docker.sh

# SageTV web servers (through plugins)
EXPOSE 80 8080

# Client (TCP 42024 for connecting, TCP 7818 for streaming, UDP 8270 for finding servers)
EXPOSE 42024 7818 8270

# All extenders (UDP 31100 for discovery, TCP 31099 for connections?)
EXPOSE 31100 31099

# Hauppage extender (all UDP)
EXPOSE 16867 16869 16881

CMD ["/work/run-docker.sh"]
#CMD /opt/sagetv/startsage && sleep infinity