FROM busybox:ubuntu-14.04
MAINTAINER Remmelt Pit <remmelt@remmelt.com>

# Install curl with ssl support
RUN (wget -O - http://www.magicermine.com/demos/curl/curl/curl-7.30.0.ermine.tar.bz2 | bunzip2 -c - | tar xf -) \
	&& mv /curl-7.30.0.ermine/curl.ermine /bin/curl \
	&& rm -Rf /curl-7.30.0.ermine

# Install jre
RUN (curl -s -k -L -C - -b "oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u20-b26/jre-8u20-linux-x64.tar.gz | tar xzf -)

ENV JAVA_HOME /jre1.8.0_20
ENV PATH $PATH:$JAVA_HOME/bin

WORKDIR /home
CMD ["java", "-version"]
