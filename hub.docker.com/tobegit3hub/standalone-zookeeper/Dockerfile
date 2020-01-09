FROM ubuntu:14.10
MAINTAINER tobe tobeg3oogle@gmail.com

RUN apt-get -y update

# Install Java7
RUN apt-get install -y software-properties-common && \
    add-apt-repository -y ppa:webupd8team/java && \
    apt-get update && \
    echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
    echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections && \
    apt-get install -y oracle-java7-installer
ENV JAVA_HOME /usr/lib/jvm/java-7-oracle/

# Install build tools
RUN apt-get install -y git && \
    apt-get install -y ant

# Install ZooKeeper
# RUN git clone git://git.apache.org/zookeeper.git /zookeeper
RUN git clone https://github.com/apache/zookeeper.git /zookeeper
WORKDIR /zookeeper
# RUN git checkout remotes/origin/branch-3.4
RUN ant
RUN cp /zookeeper/conf/zoo_sample.cfg /zookeeper/conf/zoo.cfg

# Expose port
EXPOSE 2181

CMD ["bin/zkServer.sh", "start-foreground"]
