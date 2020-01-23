FROM appertise/oracle-jdk8
MAINTAINER Appertise <appertise.co@gmail.com>

ENV MAVEN_VERSION 3.3.3

# Install and configure maven
RUN cd /tmp && \
  	wget "http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz" && \
  	tar xzf "apache-maven-$MAVEN_VERSION-bin.tar.gz" && \
  	mv /tmp/apache-maven-$MAVEN_VERSION /usr/lib && \
  	mv /usr/lib/apache-maven-$MAVEN_VERSION /usr/lib/maven && \
  	ln -s /usr/lib/maven/bin/mvn /usr/bin/mvn

VOLUME /repository

ENV MAVEN_HOME /usr/lib/maven

ENV MAVEN_OPTS -Dmaven.repo.local=/repository


# Install Jrebel
RUN mkdir /jrebel
COPY ./jrebel /jrebel

ENV REBEL_HOME /jrebel

CMD ["mvn"]
