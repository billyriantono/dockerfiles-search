FROM cogniteev/oracle-java:java6
MAINTAINER Adriano de Souza "souzadriano@gmail.com"

# Define working directory.
WORKDIR /data

# Installs Ant
ENV ANT_VERSION 1.9.12
RUN cd && \
    wget -q http://www.us.apache.org/dist//ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz && \
    tar -xzf apache-ant-${ANT_VERSION}-bin.tar.gz && \
    mv apache-ant-${ANT_VERSION} /opt/ant && \
    rm apache-ant-${ANT_VERSION}-bin.tar.gz
ENV ANT_HOME /opt/ant
ENV PATH ${PATH}:/opt/ant/bin

RUN cd && \
    apt-get update && \
    apt-get install -y curl libc6 libcurl3 zlib1g && \
    apt-get -y install git

# Define default command.
CMD ["bash"]
