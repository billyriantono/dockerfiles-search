FROM phusion/baseimage:0.9.16
MAINTAINER Ahmad Iqbal <ahmad@aurorasolutions.io>

CMD ["/sbin/my_init"]

ENV java_version 1.8.0_25
ENV filename jdk-8u25-linux-x64.tar.gz
ENV downloadlink http://download.oracle.com/otn-pub/java/jdk/8u25-b17/$filename -O /tmp/$filename
ENV JAVA_HOME /usr/lib/jvm/jdk$java_version
ENV PATH $JAVA_HOME/bin:$PATH

# Download Install utilities
RUN apt-get update && apt-get install -y unzip wget && apt-get clean

#Download java
RUN wget --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" $downloadlink -O /tmp/$filename
RUN mkdir /usr/lib/jvm && tar -zxf /tmp/$filename -C /usr/lib/jvm/
RUN update-alternatives --install /usr/bin/java java $JAVA_HOME/bin/java 20000 && update-alternatives --install /usr/bin/javac javac $JAVA_HOME/bin/javac 20000

# Clean up APT.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
