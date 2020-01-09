# Arduino IDE Builder - Linux 64
#
# Version	1.0

FROM		ubuntu:14.04
MAINTAINER	Calvin Sangbin Park <calvinspark@gmail.com>

# Use bash. I like bash.
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Install the dependencies.
RUN apt-get update && \
    apt-get install -y \
        ant \
        openjdk-7-jdk \
        unzip \
        xz-utils && \
    apt-get clean

# Set up JDK
ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64
