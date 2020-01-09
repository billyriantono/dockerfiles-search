# The Oracle JDK7 installation is shamelessly copied from 
# somebody else. I don't remember whom, and for this I deeply
# apologize. Thank you for your help, kind sir.
#
# lots of boilerplate for using phusion/baseimage from here:
# https://github.com/phusion/baseimage-docker#using
#
FROM phusion/baseimage:0.9.15
MAINTAINER Ryan Baldwin <ryanbaldwin@gmail.com>
 
# Set correct env variables
ENV TERM vt100
 
# install system deps
RUN sed -i 's/main$/main universe/' /etc/apt/sources.list \
    && apt-get -y -qq --force-yes update \
    && apt-get -y -qq --force-yes install software-properties-common
 
# install oracle jdk
ENV JDK_INST oracle-java7-installer
ENV JDK_LIC shared/accepted-oracle-license-v1-1
ENV JDK ${JDK_INST} ${JDK_LIC} select true
RUN add-apt-repository -y ppa:webupd8team/java \
    && echo ${JDK} | /usr/bin/debconf-set-selections \
    && apt-get -y -qq --force-yes update \
    && apt-get -y -qq --force-yes install oracle-java7-installer
 
# system environment variables
ENV JAVA_HOME /usr/lib/jvm/java-7-oracle
