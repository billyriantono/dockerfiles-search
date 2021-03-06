# Creates pseudo distributed hadoop 2.5.1
# Debian:lastest Wheezy
# docker build -t meabed/hadoop .

FROM debian:latest
MAINTAINER Mohamed Meabed "mo.meabed@gmail.com"

USER root
ENV DEBIAN_FRONTEND noninteractive

# Download and Install JDK / Hadoop
ENV JDK_VERSION 7
ENV HADOOP_VERSION 2.5.1


# install dev tools
RUN apt-get update
RUN apt-get install -y apt-utils
RUN apt-get install -y curl tar sudo openssh-server openssh-client rsync

# passwordless ssh
RUN rm /etc/ssh/ssh_host_dsa_key /etc/ssh/ssh_host_rsa_key

RUN ssh-keygen -q -N "" -t dsa -f /etc/ssh/ssh_host_dsa_key
RUN ssh-keygen -q -N "" -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -q -N "" -t rsa -f /root/.ssh/id_rsa

RUN cp /root/.ssh/id_rsa.pub /root/.ssh/authorized_keys


# java
RUN apt-get install -y openjdk-$JDK_VERSION-jdk

ENV JAVA_HOME /usr/lib/jvm/java-$JDK_VERSION-openjdk-amd64
ENV PATH $PATH:$JAVA_HOME/bin


# hadoop
RUN mkdir -p /opt/downloads && cd /opt/downloads && curl -SsfLO "http://www.eu.apache.org/dist/hadoop/common/hadoop-$HADOOP_VERSION/hadoop-$HADOOP_VERSION.tar.gz"
RUN cd /opt && tar xvfz /opt/downloads/hadoop-$HADOOP_VERSION.tar.gz
RUN ln -s /opt/hadoop-$HADOOP_VERSION /opt/hadoop

ENV HADOOP_PREFIX /opt/hadoop
ENV HADOOP_HOME /opt/hadoop


RUN sed -i "/^export JAVA_HOME/ s:.*:export JAVA_HOME=$JAVA_HOME\nexport HADOOP_PREFIX=$HADOOP_PREFIX\nexport HADOOP_HOME=$HADOOP_HOME\n:" $HADOOP_PREFIX/etc/hadoop/hadoop-env.sh

RUN sed -i "/^export HADOOP_CONF_DIR/ s:.*:export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop/:" $HADOOP_PREFIX/etc/hadoop/hadoop-env.sh
#RUN . $HADOOP_PREFIX/etc/hadoop/hadoop-env.sh

RUN mkdir $HADOOP_PREFIX/input
RUN cp $HADOOP_PREFIX/etc/hadoop/*.xml $HADOOP_PREFIX/input

# pseudo distributed
ADD core-site.xml.template $HADOOP_PREFIX/etc/hadoop/core-site.xml.template
RUN sed s/HOSTNAME/localhost/ $HADOOP_PREFIX/etc/hadoop/core-site.xml.template > $HADOOP_PREFIX/etc/hadoop/core-site.xml
ADD hdfs-site.xml $HADOOP_PREFIX/etc/hadoop/hdfs-site.xml

ADD mapred-site.xml $HADOOP_PREFIX/etc/hadoop/mapred-site.xml
ADD yarn-site.xml $HADOOP_PREFIX/etc/hadoop/yarn-site.xml

RUN $HADOOP_PREFIX/bin/hdfs namenode -format

# fixing the libhadoop.so like a boss

RUN rm  $HADOOP_PREFIX/lib/native/*
RUN curl -Ls http://dl.bintray.com/meabed/hadoop-debian/hadoop-native-64-2.5.1.tar|tar -x -C $HADOOP_PREFIX/lib/native/

ADD ssh_config /root/.ssh/config
RUN chmod 600 /root/.ssh/config
RUN chown root:root /root/.ssh/config


ADD bootstrap.sh /etc/bootstrap.sh
RUN chown root:root /etc/bootstrap.sh
RUN chmod 700 /etc/bootstrap.sh

ENV BOOTSTRAP /etc/bootstrap.sh

# workingaround docker.io build error
RUN ls -la $HADOOP_PREFIX/etc/hadoop/*-env.sh
RUN chmod +x $HADOOP_PREFIX/etc/hadoop/*-env.sh
RUN ls -la $HADOOP_PREFIX/etc/hadoop/*-env.sh

# fix the 254 error code
RUN sed  -i "/^[^#]*UsePAM/ s/.*/#&/"  /etc/ssh/sshd_config
RUN echo "UsePAM no" >> /etc/ssh/sshd_config
RUN echo "Port 2122" >> /etc/ssh/sshd_config

RUN service ssh start && $HADOOP_PREFIX/etc/hadoop/hadoop-env.sh && $HADOOP_PREFIX/sbin/start-dfs.sh && $HADOOP_PREFIX/bin/hdfs dfs -mkdir -p /user/root
RUN service ssh start && $HADOOP_PREFIX/etc/hadoop/hadoop-env.sh && $HADOOP_PREFIX/sbin/start-dfs.sh && $HADOOP_PREFIX/bin/hdfs dfs -put $HADOOP_PREFIX/etc/hadoop/ input

CMD ["/etc/bootstrap.sh", "-d"]

EXPOSE 50020 50090 50070 50010 50075 8031 8032 8033 8040 8042 49707 22 8088 8030
