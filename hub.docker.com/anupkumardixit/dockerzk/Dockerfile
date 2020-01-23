#===========================================
# Version:         1.8.3
# API version:     1.20
# ==========================================
FROM ubuntu:14.04
#ENV JAVA_HOME /usr/local/java/jdk1.8.0_51
MAINTAINER Anup Dixit <anupkumardixit@gmail.com>

RUN apt-get -y update && apt-get clean
# RUN apt-get -y upgrade

#=========== 1. Java setup===========
RUN apt-get install software-properties-common -y
RUN add-apt-repository ppa:webupd8team/java -y
RUN apt-get update
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN apt-get install oracle-java8-installer -y
RUN apt-get install oracle-java8-set-default -y

# ========== 2. Install Ant ========== 
RUN apt-get -y install ant

# ========= 3. Install git ===========
RUN apt-get -y install git

# ======== 4. Install Maven ==========
RUN apt-get -y install maven

EXPOSE 2181 2888 3888

RUN mkdir /tmp/zookeeper
WORKDIR /tmp/zookeeper

RUN git clone https://github.com/apache/zookeeper.git .
RUN git checkout release-3.5.1-rc2

RUN ant jar
RUN cp /tmp/zookeeper/conf/zoo_sample.cfg /tmp/zookeeper/conf/zoo.cfg
RUN echo "standaloneEnabled=false" >> /tmp/zookeeper/conf/zoo.cfg
RUN echo "dynamicConfigFile=/tmp/zookeeper/conf/zoo.cfg.dynamic" >> /tmp/zookeeper/conf/zoo.cfg ADD zk-init.sh /usr/local/bin/
ENTRYPOINT ["/usr/local/bin/zk-init.sh"]
CMD ["start-foreground"]
