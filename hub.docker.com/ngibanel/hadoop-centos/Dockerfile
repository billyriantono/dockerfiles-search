FROM nimmis/java-centos:openjdk-8-jre
MAINTAINER Nicolas Gibanel <mail@ngibanel.me>

# JAVA
ENV JAVA_HOME=/etc/alternatives/jre_1.8.0_openjdk
ENV PATH=$PATH:JAVA_HOME/bin

# Version
ENV HADOOP_VERSION=2.7.3

# Hadoop home and user
ENV HADOOP_HOME=/usr/local/hadoop-$HADOOP_VERSION
ENV HADOOP_USER=hadoop

# Install dev tools
RUN yum clean all; \
    rpm --rebuilddb; \
    yum install -y curl which tar sudo openssh-server openssh-clients rsync

# Update libselinux
RUN yum update -y libselinux

# Install Hadoop
RUN mkdir -p "${HADOOP_HOME}" \ 
    && export ARCHIVE=hadoop-$HADOOP_VERSION.tar.gz \
    && export DOWNLOAD_PATH=dist/hadoop/common/hadoop-$HADOOP_VERSION/$ARCHIVE \
    && curl -s http://www.eu.apache.org/$DOWNLOAD_PATH | \
        tar -xz -C $HADOOP_HOME --strip-components 1 \
    && rm -rf $ARCHIVE

# HDFS Volume
VOLUME /opt/hdfs

# add user
RUN useradd -s /bin/bash $HADOOP_USER

# Paths
ENV HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
ENV HADOOP_LIBEXEC_DIR=$HADOOP_HOME/libexec
ENV PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin

# Copy configuration
COPY /conf/*.xml $HADOOP_CONF_DIR/

# fix configuration file
RUN sed  -i.bak "s/hadoop-daemons.sh/hadoop-daemon.sh/g" \
        $HADOOP_HOME/sbin/start-dfs.sh \
    && rm -f $HADOOP_HOME/sbin/start-dfs.sh.bak \
    && sed -i.bak "s/hadoop-daemons.sh/hadoop-daemon.sh/g" \
        $HADOOP_HOME/sbin/stop-dfs.sh \
    && rm -f $HADOOP_HOME/sbin/stop-dfs.sh.bak

# HDFS
EXPOSE 8020 14000 50070 50470

# MapReduce
EXPOSE 10020 13562 19888

# Copy start scripts
COPY start-hadoop /opt/util/bin/start-hadoop
COPY start-hadoop-namenode /opt/util/bin/start-hadoop-namenode
COPY start-hadoop-datanode /opt/util/bin/start-hadoop-datanode
ENV PATH=$PATH:/opt/util/bin

# Fix permissions
RUN chown -R $HADOOP_USER.$HADOOP_USER /opt/hdfs
RUN chown -R $HADOOP_USER.$HADOOP_USER $HADOOP_HOME

# passwordless ssh
RUN mkdir -p /home/$HADOOP_USER/.ssh
RUN ssh-keygen -q -N "" -t dsa -f /etc/ssh/ssh_host_dsa_key
RUN ssh-keygen -q -N "" -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -q -N "" -t rsa -f /home/$HADOOP_USER/.ssh/id_rsa
RUN cp /home/$HADOOP_USER/.ssh/id_rsa.pub /home/$HADOOP_USER/.ssh/authorized_keys

ADD ssh_config /home/$HADOOP_USER/.ssh/config
RUN chmod 600 /home/$HADOOP_USER/.ssh/config
RUN chown $HADOOP_USER.$HADOOP_USER /home/$HADOOP_USER/.ssh/config

# Fix environment for other users
RUN echo "export HADOOP_HOME=$HADOOP_HOME" > /etc/bashrc.tmp \
    && echo "export HADOOP_USER=$HADOOP_USER" > /etc/bashrc.tmp \
    && echo "export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:/opt/util/bin" >> /etc/bashrc.tmp \    
    && cat /etc/bashrc >> /etc/bashrc.tmp \
    && mv -f /etc/bashrc.tmp /etc/bashrc