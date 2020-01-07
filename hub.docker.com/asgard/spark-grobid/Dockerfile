# base
FROM asgard/spark

# utils
RUN apt-get update && apt-get install -y unzip

# Maven
RUN \
  export DEBIAN_FRONTEND=noninteractive && \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y --no-install-recommends software-properties-common && \
  apt-get install -y vim maven libxml2

# Scala (https://github.com/hseeberger/scala-sbt/blob/master/Dockerfile)
ENV SCALA_VERSION 2.10.5
RUN \
  curl -fsL http://downloads.typesafe.com/scala/$SCALA_VERSION/scala-$SCALA_VERSION.tgz | tar xfz - -C /root/ && \
  echo >> /root/.bashrc && \
  echo 'export PATH=~/scala-$SCALA_VERSION/bin:$PATH' >> /root/.bashrc

# SBT
RUN \
  echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list && \
  apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 642AC823 && \
  apt-get -y update && \
  apt-get install -y sbt

# Grobid
RUN wget https://github.com/kermitt2/grobid/archive/grobid-parent-0.4.1.zip \
  && unzip grobid-parent-0.4.1.zip \
  && mv grobid-grobid-parent-0.4.1 grobid \
  && cd grobid \
  && mvn -DskipTests=true clean install

# grobid env variable
ENV GROBID_HOME /grobid/grobid-home
ENV GROBID_CORE /grobid/grobid-core

WORKDIR /home

###########################################################################
# Init Setup Script
###########################################################################

# au cas ou
# RUN chmod +x init_script
ENTRYPOINT ["/sbin/init_script"]

# clean docker
# uninstall maven :)
RUN apt-get autoremove -y \
  && apt-get -y autoremove maven \
  && apt-get clean -y \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
