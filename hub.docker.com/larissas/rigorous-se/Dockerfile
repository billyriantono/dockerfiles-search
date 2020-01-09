# =================================================================
# DO NOT MODIFY THIS FILE (we will overwrite this file for grading)
# =================================================================
#
# Specification for docker image
#
# Compile using:
# ./prepare.sh

FROM ubuntu:bionic
# Ubuntu 18.04


# install basic prerequisites
RUN apt-get update && apt-get install -y \
		build-essential \
		wget \
		git \
		tar \
		vim \
		sed \
		python3 \
		python3-pip
RUN pip3 install pandas

# install basic APRON prerequisites (following https://github.com/antoinemine/apron)
RUN apt-get update && apt-get install -y \
		gcc \
		libgmp3-dev \
		libmpfr-dev \
		perl \
		sed


# Install Java 1.8
RUN apt-get update && apt-get install -y openjdk-8-jdk

# Define environment variables
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64

ENV JAVA $JAVA_HOME/bin/java
ENV JAVAC $JAVA_HOME/bin/javac


RUN mkdir -p /opt

# install PPL (another APRON prerequisite): https://www.bugseng.com/ppl-download
RUN apt-get update && apt-get install -y m4 && \
		mkdir /opt/ppl && cd /opt/ppl && \
		wget -q -O ./ppl-1.2.tar.bz2 http://www.bugseng.com/products/ppl/download/ftp/releases/1.2/ppl-1.2.tar.bz2 && \
		tar xjf ./ppl-1.2.tar.bz2 && \
		cd ./ppl-1.2 && \
		./configure && \
		make && \
		make install

# install APRON: https://github.com/antoinemine/apron
# the `sed` command sets `JNIINC` in `Makefile.config` to `-I/include -I$JAVA_HOME/include -I$JAVA_HOME/include/linux`
# the `cat` command displays the resulting `Makefile.config`
RUN cd /opt && \
		git clone https://github.com/antoinemine/apron.git && \
		cd apron && \
		JAVA_HOME=$JAVA_HOME ./configure && \
		cat Makefile.config && \
		sed -i -e "s#JNIINC    = -I/include#JNIINC    = -I/include -I$JAVA_HOME/include -I$JAVA_HOME/include/linux#g" Makefile.config && \
		cat Makefile.config && \
		make && \
		make install


ENV APRON /opt/apron