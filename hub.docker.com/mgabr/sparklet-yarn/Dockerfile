#
# Spark on YARN and Hadoop Standalone Container
# Apache Spark 2.4.4, Hadoop 2.6
#
# Runs Spark on a pseudo distributed YARN cluster in a container
# Suitable for building test/development containers for Spark apps interacting with YARN and HDFS
#
# Takes some time to start HDFS, in scripts you can use sleep 30
#
# Usage:
# $ docker build -t mgabr/sparklet-yarn:2.4.4 -f Dockerfile-yarn .
# $ docker run -p 8080:8080 -p 50070:50070 -it mgabr/sparklet-yarn:2.4.4

FROM anapsix/alpine-java:latest
LABEL author="Markus Gabriel"

# spark web admin ports
EXPOSE 4040
EXPOSE 8080

# spark debugging port
EXPOSE 9999

# hadoop web admin ports
EXPOSE 50070

WORKDIR /opt

RUN \
  # grab curl and ssh
  apk --no-cache add openssh vim curl procps && \
  curl https://archive.apache.org/dist/spark/spark-2.4.4/spark-2.4.4-bin-hadoop2.6.tgz > spark.tgz && \
  # generate a keypair and authorize it
  mkdir -p /root/.ssh && \
  ssh-keygen -f /root/.ssh/id_rsa -N "" && \
  cat /root/.ssh/id_rsa.pub > /root/.ssh/authorized_keys && \
  # extract spark
  tar -xzf spark.tgz && \
  # cleanup spark tarball
  rm spark.tgz && \
  # s6 overlay
  curl -LS https://github.com/just-containers/s6-overlay/releases/download/v1.17.2.0/s6-overlay-amd64.tar.gz -o /tmp/s6-overlay.tar.gz && \
  tar xvfz /tmp/s6-overlay.tar.gz -C / && \
  rm -f /tmp/s6-overlay.tar.gz && \
  # generate host keys
  ssh-keygen -A && \
  curl https://archive.apache.org/dist/hadoop/common/hadoop-2.6.5/hadoop-2.6.5.tar.gz > hadoop.tar.gz && \
  # extract hadoop
  tar -xzf hadoop.tar.gz && \
  # cleanup hadoop tarball
  rm hadoop.tar.gz

# add ssh config to disable host key checking
ADD config/ssh-config /root/.ssh/config

# add hadoop and yarn config
ADD config/core-site.xml /opt/hadoop-2.6.5/etc/hadoop/core-site.xml
ADD config/hdfs-site.xml /opt/hadoop-2.6.5/etc/hadoop/hdfs-site.xml
ADD config/mapred-site.xml /opt/hadoop-2.6.5/etc/hadoop/mapred-site.xml
ADD config/yarn-site.xml /opt/hadoop-2.6.5/etc/hadoop/yarn-site.xml

# upload init scripts
ADD services/hadoop-init /etc/cont-init.d/hadoop
ADD services/yarn-init /etc/cont-init.d/yarn

# fix JAVA_HOME not found in hadoop
RUN echo "export JAVA_HOME="$JAVA_HOME >> /opt/hadoop-2.6.5/etc/hadoop/hadoop-env.sh

ENV HADOOP_CONF_DIR /opt/hadoop-2.6.5/etc/hadoop
ENV YARN_CONF_DIR /opt/hadoop-2.6.5/etc/hadoop
ENV PATH /opt/spark-2.4.4-bin-hadoop2.6/bin:/opt/hadoop-2.6.5/bin:/opt/hadoop-2.6.5/sbin:$PATH

# add environment variables for spark
RUN echo "export HADOOP_CONF_DIR="$HADOOP_CONF_DIR >> /opt/spark-2.4.4-bin-hadoop2.6/conf/spark-env.sh && \
  echo "export YARN_CONF_DIR="$YARN_CONF_DIR >> /opt/spark-2.4.4-bin-hadoop2.6/conf/spark-env.sh && \
  chmod a+x /opt/spark-2.4.4-bin-hadoop2.6/conf/spark-env.sh

ENTRYPOINT [ "/init" ]

CMD ["spark-shell"]
