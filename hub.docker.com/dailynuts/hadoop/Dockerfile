#   Copyright 2019 The Kubernetes Authors.
#
#   Licensed under the Apache License, Version 2.0 (the "License");
#   you may not use this file except in compliance with the License.
#   You may obtain a copy of the License at
#
#       http://www.apache.org/licenses/LICENSE-2.0
#
#   Unless required by applicable law or agreed to in writing, software
#   distributed under the License is distributed on an "AS IS" BASIS,
#   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#   See the License for the specific language governing permissions and
#   limitations under the License.

FROM ubuntu:18.04

ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
ENV HADOOP_DATA_DIR=/var/lib/hadoop
ENV HADOOP_LOG_DIR=/var/log/hadoop
ENV HADOOP_GROUP=hadoop
ENV HADOOP_HDFS_USER=hdfs
ENV HADOOP_YARN_USER=yarn
ENV HADOOP_MAPRED_USER=mapred

# The ARG instruction defines a variable that users can pass at build-time
# to the builder with the docker build command using the
# --build-arg <varname>=<value> flag.
ARG HADOOP_DIST=hadoop-3.2.1

RUN set -x \
    && apt-get update \
    && apt-get install -y openjdk-8-jre-headless curl ssh pdsh \
    && curl -fSL "https://mirrors.tuna.tsinghua.edu.cn/apache/hadoop/common/${HADOOP_DIST}/${HADOOP_DIST}.tar.gz" -o hadoop.tar.gz \
    && tar -xz -f hadoop.tar.gz -C /opt \
    && rm -rf hadoop.tar.gz \
    && ln -s /opt/${HADOOP_DIST}/etc/hadoop /etc/hadoop \
    && rm -rf /var/lib/apt/lists/*


#Copy configuration generator script to bin
COPY scripts /usr/local/bin/

# Create a user for the hadoop process and configure file system ownership
# for nessecary directories and symlink the distribution as a user executable
RUN set -x \
	&& groupadd $HADOOP_GROUP \
	&& useradd $HADOOP_HDFS_USER -g $HADOOP_GROUP \
	&& useradd $HADOOP_YARN_USER -g $HADOOP_GROUP \
	&& useradd $HADOOP_MAPRED_USER -g $HADOOP_GROUP \
	&& mkdir -p $HADOOP_DATA_DIR $HADOOP_LOG_DIR \
	&& chown -R "$HADOOP_HDFS_USER:$HADOOP_GROUP" $HADOOP_DATA_DIR $HADOOP_LOG_DIR /etc/hadoop /opt/${HADOOP_DIST} \
	&& ln -s /opt/${HADOOP_DIST}/bin/* /usr/local/bin