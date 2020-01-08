FROM haidong/java
MAINTAINER haidong <383623085@qq.com>

# Set environment variables for program versions
ARG HADOOP_VERSION=2.7.3
ENV HADOOP_INSTALL=/opt/hadoop
ENV PATH $PATH:$HADOOP_INSTALL/bin:$HADOOP_INSTALL/sbin

# Change to tmp folder
WORKDIR /tmp

# SSH Key Passwordless
RUN apt-get update && apt-get install -y ssh \
    && ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa \
    && cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys \
    && chmod 0600 ~/.ssh/authorized_keys

# Config SSH and ENV
RUN sed -i '/StrictHostKeyChecking/s/#//g' /etc/ssh/ssh_config \
    && sed -i '/StrictHostKeyChecking/s/ask/no/g' /etc/ssh/ssh_config

RUN sed -i 'i JAVA_HOME=/opt/java' /etc/environment \
	&& sed -i 'i HADOOP_INSTALL=/opt/hadoop' /etc/environment \
	&& sed -i '/^PATH/s:"$:\:/opt/java/bin\:/opt/hadoop/bin\:/opt/hadoop/sbin":' /etc/environment

# Download and extract hadoop to opt folder
RUN curl -L http://mirrors.tuna.tsinghua.edu.cn/apache/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz \    
    | tar -zx -C /opt \
    && ln -s /opt/hadoop-${HADOOP_VERSION} /opt/hadoop
	
# Config Hadoop
COPY entrypoint.sh ${HADOOP_INSTALL}
COPY conf  ${HADOOP_INSTALL}/etc/hadoop/
RUN chmod +x ${HADOOP_INSTALL}/entrypoint.sh

# EXPOSE 22 50070 19888 8088 50075

# Hdfs ports
EXPOSE 50010 50020 50070 50075 50090 8020 9000

# Mapred ports
EXPOSE 10020 19888

# Yarn ports
EXPOSE 8030 8031 8032 8033 8040 8042 8088

# Other ports
EXPOSE 22

# Change to root folder
WORKDIR /root

ENTRYPOINT ["/opt/hadoop/entrypoint.sh"]
