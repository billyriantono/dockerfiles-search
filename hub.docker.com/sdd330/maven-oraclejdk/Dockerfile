FROM frolvlad/alpine-oraclejdk8

MAINTAINER yang.leijun@gmail.com

# Install packages
RUN apk add --update bash curl && rm -rf /var/cache/apk/*

# Install maven
ENV MAVEN_VERSION 3.3.3

RUN curl -fsSL http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz | tar xzf - -C /usr/share \
  && mv /usr/share/apache-maven-$MAVEN_VERSION /usr/share/maven \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

ENV MAVEN_HOME /usr/share/maven

# Define mount point to access data on host system.
VOLUME ["/workspace"]

# Command
CMD ["mvn"]
