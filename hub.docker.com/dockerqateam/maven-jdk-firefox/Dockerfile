FROM ubuntu:latest

RUN set -x \
   && apt-get update \
   && apt-get install -y \
       locales
RUN apt-get -y install curl
##################
# Install Java 8#
##################
ENV LC_ALL C.UTF-8
RUN locale-gen $LANG
RUN set -x \
   && apt-get update \
   && apt-get install -y \
       ca-certificates-java \
       openjdk-8-jre-headless \
       openjdk-8-jre \
       openjdk-8-jdk-headless \
       openjdk-8-jdk
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
RUN export JAVA_HOME
#################
# Install maven#
#################
ENV MAVEN_VERSION 3.6.1
RUN mkdir -p /usr/share/maven \
 && curl -fsSL http://apache.osuosl.org/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz \
   | tar -xzC /usr/share/maven --strip-components=1 \
 && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn
ENV MAVEN_HOME /usr/share/maven
VOLUME /root/.m2
##################
# install firefox#
##################
ENV FIREFOX_VERSION 70.0
ENV FIREFOX_DOWNLOAD https://download.mozilla.org/?product=firefox-$FIREFOX_VERSION-SSL&os=linux64
RUN apt-get update && apt-get install -y \
  wget bzip2 libgtk-3-0 pulseaudio libdbus-glib-1-2 libxt6 \
  && apt-get clean
RUN wget -O - -q "$FIREFOX_DOWNLOAD" > firefox.tar \
&& tar xvjf firefox.tar \
&& mv firefox/ /opt/ \
&&  ln -s /opt/firefox/firefox /usr/local/bin/firefox
######################
#Install XVFB display#
######################
RUN apt-get -y install xvfb gtk2-engines-pixbuf
ENV DISPLAY=:99
##############
#Run firefox#
#############
#RUN firefox -v
