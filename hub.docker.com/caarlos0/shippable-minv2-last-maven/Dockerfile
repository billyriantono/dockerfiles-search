# shippable/minv2 image with last maven version (3.3.1)
FROM shippable/minv2
MAINTAINER Carlos Alexandro Becker <caarlos0@gmail.com>

RUN sudo apt-get remove -y maven && \
  wget -O /tmp/maven.tar.gz http://mirror.nbtelecom.com.br/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.tar.gz && \
  tar xzvf /tmp/maven.tar.gz -C /opt && \
  ln -s /opt/apache-maven-3.3.1/bin/mvn /usr/bin/mvn && \
  rm -rf /tmp/maven.tar.gz

ENV M2_HOME /opt/apache-maven-3.3.1 \
    PATH $M2_HOME/bin:$PATH
