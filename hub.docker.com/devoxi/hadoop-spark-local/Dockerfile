FROM ubuntu:14.04
MAINTAINER Olivier Devoisin (devoxi.git@outlook.com)

# System upgrade
RUN apt-get update
#RUN apt-get upgrade -y

# Tools installation
RUN apt-get install -y vim htop

# Java installation
RUN apt-get install -y openjdk-7-jre openjdk-7-jdk
ENV JAVA_HOME /usr/lib/jvm/jdk
RUN ln -s /usr/lib/jvm/java-7-openjdk-amd64 $JAVA_HOME

# SSH installation
RUN apt-get install -y ssh rsync
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN sed -i '/Port 22/c\Port 40022' /etc/ssh/sshd_config

# Hadoop installation
ADD http://www.apache.org/dist/hadoop/core/hadoop-2.6.2/hadoop-2.6.2.tar.gz /
RUN tar -xzf hadoop-2.6.2.tar.gz
RUN mv /hadoop-2.6.2 /hadoop
RUN rm -rf hadoop-2.6.2.tar.gz
ADD core-site.xml /hadoop/etc/hadoop/core-site.xml
ADD hdfs-site.xml /hadoop/etc/hadoop/hdfs-site.xml
ADD yarn-site.xml /hadoop/etc/hadoop/yarn-site.xml
ADD mapred-site.xml /hadoop/etc/hadoop/mapred-site.xml
RUN sed -i '/export JAVA_HOME=${JAVA_HOME}/c\export JAVA_HOME=/usr/lib/jvm/jdk' /hadoop/etc/hadoop/hadoop-env.sh

# Spark installation
ADD http://www.apache.org/dist/spark/spark-1.5.2/spark-1.5.2-bin-hadoop2.6.tgz /
RUN tar -xzf spark-1.5.2-bin-hadoop2.6.tgz
RUN mv /spark-1.5.2-bin-hadoop2.6 /spark
RUN rm -rf spark-1.5.2-bin-hadoop2.6.tgz

# Hadoop user creation
RUN addgroup hadoop
RUN useradd -d /home/hduser -m -s /bin/bash -G hadoop hduser
RUN sudo adduser hduser sudo
RUN echo 'hduser:hduser' | chpasswd

# SSH config
RUN su hduser -c "ssh-keygen -t rsa -f ~/.ssh/id_rsa -P ''"
RUN su hduser -c "cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys"
ADD ssh_config ./ssh_config
RUN mv ./ssh_config /home/hduser/.ssh/config

# Launch scripts
ENV PATH=$PATH:/hadoop/bin:/spark/bin:$JAVA_HOME
ENV HADOOP_CLASSPATH=${JAVA_HOME}/lib/tools.jar
ENV HADOOP_CONF_DIR=/hadoop/etc/hadoop
ADD starthadoop.sh /home/hduser/starthadoop.sh
RUN chmod 700 /home/hduser/starthadoop.sh

# Code examples
ADD examples /home/hduser/examples

# Permissions
RUN chown -R hduser:hduser /home/hduser
RUN chmod 700 /home/hduser/.ssh ; chmod 600 /home/hduser/.ssh/authorized_keys ; chmod go-wrx /home/hduser
RUN chown -R hduser:hduser /hadoop
RUN chown -R hduser:hduser /spark
ADD hduser-sudoer /etc/sudoers.d/hduser-sudoer

# Select workdir and user
WORKDIR /home/hduser
USER hduser
