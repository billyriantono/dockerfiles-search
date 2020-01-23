FROM endle/travis-simulate-docker

MAINTAINER Zhenbo Li

#To Edit PPA
RUN apt-get update -qq
RUN apt-get install -y python-software-properties

#Fix KEY Problems
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 5A9A06AEF9CB8DB0

#Install wine(Should be latest)
RUN add-apt-repository -y ppa:ubuntu-wine/ppa
RUN apt-get update -qq
RUN apt-get install -y wine1.7

#Install cross-compile tools
RUN apt-get install -y binutils-mingw-w64-i686
RUN apt-get install -y gcc-mingw-w64-i686

