#
# Licensed to the Apache Software Foundation (ASF) under one or more
# contributor license agreements.  See the NOTICE file distributed with
# this work for additional information regarding copyright ownership.
# The ASF licenses this file to You under the Apache License, Version 2.0
# (the "License"); you may not use this file except in compliance with
# the License.  You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

FROM ubuntu:trusty
MAINTAINER Yu Ishikawa

# Set environment variables.
ENV DEBIAN_FRONTEND="noninteractive" \
    DEBCONF_NONINTERACTIVE_SEEN="true" \
    LC_ALL="C"

# Upgrade package index and install basic commands.
RUN apt-get update && \
    apt-get install -y git less net-tools openssh-server time \
        software-properties-common python-software-properties \
        python-numpy cython python-scipy

# Install Java.
RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    add-apt-repository ppa:webupd8team/java -y && \
    apt-get update && \
    apt-get install -y oracle-java7-installer && \
    update-alternatives --display java && \ 
    export JAVA_HOME=/usr/lib/jvm/java-7-oracle && \
    apt-get upgrade -y && \
    apt-get clean

# Install Scala.
ENV SCALA_VERSION 2.10.4 
ENV SCALA_HOME /opt/scala-$SCALA_VERSION 
ENV PATH $SPARK_HOME:$SCALA_HOME/bin:$PATH
ADD http://www.scala-lang.org/files/archive/scala-$SCALA_VERSION.tgz /
RUN (cd / && gunzip < scala-$SCALA_VERSION.tgz)|(cd /opt && tar -xvf -) && \
    rm /scala-$SCALA_VERSION.tgz

# Clone and compile the master branch of Apache Spark
ENV SPARK_HOME /opt/spark
RUN git clone https://github.com/apache/spark.git /opt/spark && \
    cd /opt/spark && \
    ./sbt/sbt clean assembly
