# Pull base image.
FROM ubuntu:15.04

# Install Java.
RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  apt-get install --no-install-recommends -y software-properties-common && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer

# Configure TimeZone
RUN sed -i 's/ZONE=.*/ZONE=Brazil\/East/g' /etc/localtime && \
    ln -sf /usr/share/zoneinfo/Brazil/East /etc/localtime

# Define working directory.
WORKDIR /data

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# Define default command.
CMD ["bash"]
