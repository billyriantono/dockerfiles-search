FROM ubuntu:12.04

RUN apt-get update -qq
RUN apt-get install -y build-essential libfuse-dev fuse-utils libcurl4-openssl-dev libxml2-dev mime-support automake libtool wget tar curl unzip software-properties-common python-software-properties

RUN wget https://github.com/s3fs-fuse/s3fs-fuse/archive/v1.77.tar.gz -O /usr/src/v1.77.tar.gz
RUN tar xvz -C /usr/src -f /usr/src/v1.77.tar.gz
RUN cd /usr/src/s3fs-fuse-1.77 && ./autogen.sh && ./configure --prefix=/usr && make && make install

RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

CMD ["bash"]
