FROM ubuntu:14.04.4

RUN apt-get update && apt-get install -y git curl zip wget unzip tar && rm -rf /var/lib/apt/lists/*

# Install JDK 8
USER root
RUN \
echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
apt-get update -y && \
apt-get install software-properties-common -y && \
add-apt-repository -y ppa:webupd8team/java
RUN apt-get update -y && \
apt-get install -y oracle-java8-installer
RUN rm -rf /var/lib/apt/lists/* && \
rm -rf /var/cache/oracle-jdk8-installer
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle


# Install Maven
ENV MAVEN_VERSION 3.2.5
RUN mkdir -p /usr/share/maven \
  && curl -fsSL http://apache.osuosl.org/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz \
    | tar -xzC /usr/share/maven --strip-components=1 \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn
ENV MAVEN_HOME /usr/share/maven
#COPY settings.xml /usr/share/maven/conf/settings.xml
VOLUME /root/.m2


# Install Python (required by Jspresso Qooxdoo builds)
RUN apt-get update \
  && apt-get install build-essential zlib1g-dev python-dev make -y \
  && wget http://www.python.org/ftp/python/2.7.1/Python-2.7.1.tgz \
  && tar -zxvf Python-2.7.1.tgz
RUN cd /Python-2.7.1 \
  && sed -i 's/#zlib zlibmodule.c/zlib zlibmodule.c/g' Modules/Setup.dist \
  && ./configure && make && make install \
  && cd / \
  && rm -fr /Python-2.7.1.tgz

# TEST zlib installation in python #>python -c "import zlib; print(zlib.__version__)"


#WORKDIR /root

#docker run -it -v "$PWD/hrsample-ce":/usr/src/mymaven -w /usr/src/mymaven jspresso_build /bin/bash
CMD ["mvn"]
