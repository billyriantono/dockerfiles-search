FROM stackbrew/debian:wheezy
MAINTAINER Alexis MP "alexis.mp@gmail.com"

# Update list of packages
RUN apt-get update

# Fake a fuse install (or openjdk-7-jdk will not install => on Ubuntu only?)
#RUN apt-get install libfuse2
#RUN cd /tmp ; apt-get download fuse
#RUN cd /tmp ; dpkg-deb -x fuse_* .
#RUN cd /tmp ; dpkg-deb -e fuse_*
#RUN cd /tmp ; rm fuse_*.deb
#RUN cd /tmp ; echo -en '#!/bin/bash\nexit 0\n' > DEBIAN/postinst
#RUN cd /tmp ; dpkg-deb -b . /fuse.deb
#RUN cd /tmp ; dpkg -i /fuse.deb

# install Java 7
RUN apt-get install -y openjdk-7-jdk

# set a bunch of environment variables
ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64/
ENV PATH $JAVA_HOME/bin:$PATH
