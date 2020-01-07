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

FROM openjdk:8-alpine

ARG spark_jars=jars
ARG img_path=kubernetes/dockerfiles
ARG k8s_tests=kubernetes/tests

# Before building the docker image, first build and make a Spark distribution following
# the instructions in http://spark.apache.org/docs/latest/building-spark.html.
# If this docker file is being used in the context of building your images from a Spark
# distribution, the docker build command should be invoked from the top level directory
# of the Spark distribution. E.g.:
# docker build -t spark:latest -f kubernetes/dockerfiles/spark/Dockerfile .

#RUN echo "http://dl-cdn.alpinelinux.org/alpine/v3.4/community" >> /etc/apk/repositories;
#RUN echo "http://dl-cdn.alpinelinux.org/alpine/v3.4/main" >> /etc/apk/repositories

RUN echo "http://mirrors.gigenet.com/alpinelinux/v3.4/community" >> /etc/apk/repositories;
RUN echo "http://mirrors.gigenet.com/alpinelinux/v3.4/main" >> /etc/apk/repositories

RUN set -ex && \
    apk upgrade --no-cache && \
    apk add --no-cache bash tini libc6-compat linux-pam nss && \
    mkdir -p /opt/spark && \
    mkdir -p /opt/spark/work-dir && \
    touch /opt/spark/RELEASE && \
    rm /bin/sh && \
    ln -sv /bin/bash /bin/sh && \
    echo "auth required pam_wheel.so use_uid" >> /etc/pam.d/su && \
    chgrp root /etc/passwd && chmod ug+rw /etc/passwd
    
RUN apk add --no-cache python && \
    apk add --no-cache python3 && \
    python -m ensurepip && \
    python3 -m ensurepip && \
    # We remove ensurepip since it adds no functionality since pip is
    # installed on the image and it just takes up 1.6MB on the image
    rm -r /usr/lib/python*/ensurepip && \
    pip install --upgrade pip setuptools && \
    # You may install with python3 packages by using pip3.6
    # Removed the .cache to save space
    rm -r /root/.cache

RUN apk add --no-cache R R-dev

#COPY ${spark_jars} /opt/spark/jars
#COPY bin /opt/spark/bin
#COPY sbin /opt/spark/sbin
#COPY ${img_path}/spark/entrypoint.sh /opt/
#COPY examples /opt/spark/examples
#COPY ${k8s_tests} /opt/spark/tests
#COPY data /opt/spark/data

#ENV SPARK_HOME /opt/spark

#WORKDIR /opt/spark/work-dir

#ENTRYPOINT [ "/opt/entrypoint.sh" ]
