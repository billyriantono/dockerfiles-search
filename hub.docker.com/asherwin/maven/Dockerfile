#
# maven build environment
#

FROM dockerfile/java:oracle-java8
MAINTAINER Alex Sherwin <alex.sherwin@acadiasoft.com>

WORKDIR /data
RUN wget -O - http://apache.cs.utah.edu/maven/maven-3/3.2.3/binaries/apache-maven-3.2.3-bin.tar.gz | gunzip -c | tar xvf -
RUN ln -s /data/apache-maven-3.2.3/bin/mvn /usr/local/bin/mvn

