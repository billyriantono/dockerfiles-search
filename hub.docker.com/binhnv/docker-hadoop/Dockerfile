FROM java:openjdk-8u72-jdk
MAINTAINER Binh Van Nguyen

# Hdfs ports
EXPOSE 50010 50020 50070 50075 50090 8020 9000
# Mapred ports
EXPOSE 19888
#Yarn ports
EXPOSE 8030 8031 8032 8033 8040 8042 8088
#Other ports
EXPOSE 49707 2122

ENV USER_NAME root
ENV USER_HOME /${USER_NAME}
ENV USER_BIN_DIR /usr/local/bin
ENV USER_SSH_DIR ${USER_HOME}/.ssh
ENV SYS_SSH_DIR /etc/ssh

ENV HD_VERSION 2.7.1
ENV HD_VERNAME hadoop-${HD_VERSION}
ENV HD_INSTALL_DIR /usr/local/hadoop
ENV HD_CONF_TPL_DIR ${HD_INSTALL_DIR}/templates

ARG HD_PACKAGE_URL=http://www.eu.apache.org/dist/hadoop/common/${HD_VERNAME}/${HD_VERNAME}.tar.gz
ARG DOCKERIZE_URL=https://github.com/jwilder/dockerize/releases/download/v0.2.0/dockerize-linux-amd64-v0.2.0.tar.gz

ARG HD_HADOOP_HEAPSIZE=256
ARG HD_YARN_HEAPSIZE=256

USER ${USER_NAME}

ENV HADOOP_PREFIX ${HD_INSTALL_DIR}
ENV HADOOP_COMMON_HOME ${HADOOP_PREFIX}
ENV HADOOP_HDFS_HOME ${HADOOP_COMMON_HOME}
ENV HADOOP_MAPRED_HOME ${HADOOP_COMMON_HOME}
ENV HADOOP_YARN_HOME ${HADOOP_COMMON_HOME}
ENV HADOOP_CONF_DIR ${HADOOP_COMMON_HOME}/etc/hadoop
# This will limit Hadoop daemons' heap size
ENV HADOOP_HEAPSIZE ${HD_HADOOP_HEAPSIZE}
# This will limit YARN daemon's heap size
ENV YARN_HEAPSIZE ${HD_YARN_HEAPSIZE}
ENV YARN_CONF_DIR ${HADOOP_COMMON_HOME}/etc/hadoop

COPY ssh/config ${USER_SSH_DIR}/config
COPY templates ${HD_INSTALL_DIR}/templates
COPY scripts/dhcmd ${USER_BIN_DIR}/dhcmd

# run it in foreground by default
CMD ["dhcmd", "start", "-f"]

RUN chmod +x ${USER_BIN_DIR}/dhcmd \
    && apt-get update \
    && apt-get install -y openssh-server libselinux1 \
    && chmod 600 ${USER_SSH_DIR}/config \
    && chown ${USER_NAME}:${USER_NAME} ${USER_SSH_DIR}/config \
    && rm -f ${USER_SSH_DIR}/id_rsa && ssh-keygen -q -N "" -t rsa -f ${USER_SSH_DIR}/id_rsa \
    && cat ${USER_SSH_DIR}/id_rsa.pub >> ${USER_SSH_DIR}/authorized_keys \
    && chmod 0600 ${USER_SSH_DIR}/authorized_keys \
# Dockerize
    && curl -sL ${DOCKERIZE_URL} | tar -zx -C ${USER_BIN_DIR} \
# Download hadoop package
    && mkdir -p ${HD_INSTALL_DIR} \
    && curl -s ${HD_PACKAGE_URL} | tar -xz -C ${HD_INSTALL_DIR} --strip-components=1 \
# Update some configuration, need to set this because some daemons are started
# over SSH and they environment variables are not set to correct values there
    && sed -i "s:^export JAVA_HOME=.*:export JAVA_HOME=${JAVA_HOME}:" ${HADOOP_CONF_DIR}/hadoop-env.sh \
    && sed -i "s:^export HADOOP_CONF_DIR=.*:export HADOOP_CONF_DIR=${HADOOP_CONF_DIR}:" ${HADOOP_CONF_DIR}/hadoop-env.sh
