# Arduino IDE Builder - Linux 32
#
# Version	1.0

FROM		32bit/ubuntu:14.04
MAINTAINER	Calvin Sangbin Park <calvinspark@gmail.com>

# Use bash. I like bash.
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Bug fix: https://bugs.launchpad.net/ubuntu/+source/systemd/+bug/1325142/comments/38
RUN dpkg-divert --local --add /etc/init.d/systemd-logind
RUN ln -s /bin/true /etc/init.d/systemd-logind

# Install the dependencies.
RUN apt-get update && \
    apt-get install -f -y \
        libpam-systemd:i386 \
        ant \
        openjdk-7-jdk \
        unzip \
        xz-utils && \
    apt-get clean

# Set up JDK
ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-i386
