# Get latest OS
FROM alpine:latest
RUN apk update
RUN apk upgrade

# Some basic tools
RUN apk add bash
RUN apk add nano
RUN apk add htop

# Install Java
RUN apk add openjdk7-jre
ENV JAVA_HOME /usr/lib/jvm/default-jvm

# Install Jython
RUN mkdir /usr/local/lib/jython
RUN wget -O /usr/local/lib/jython/jython.jar "http://central.maven.org/maven2/org/python/jython-standalone/2.7.1b1/jython-standalone-2.7.1b1.jar"
ADD python.sh /usr/local/bin/python
RUN chmod +x /usr/local/bin/python

# Clean up
RUN rm -rf /var/cache/apk/*
