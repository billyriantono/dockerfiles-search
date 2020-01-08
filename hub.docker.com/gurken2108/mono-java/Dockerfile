FROM phusion/baseimage:latest
MAINTAINER info@the-town.net

RUN apt-get update -qq && \
  apt-get upgrade -qqy && \
  apt-get install -qqy software-properties-common aptitude && \
  apt-add-repository -y ppa:git-core/ppa && \
  apt-get update -qq && \
  apt-get upgrade -qqy && \
  apt-get install -qqy git curl unzip wget doxygen && \
  rm -rf /var/lib/apt/lists/*

# java
RUN apt-add-repository -y ppa:webupd8team/java && \
  apt-get update -qq && \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | tee /etc/oracle-java-8-licence-acceptance | /usr/bin/debconf-set-selections && \
  apt-get install -qqy oracle-java8-installer ca-certificates oracle-java8-set-default maven && \
  rm -rf /var/lib/apt/lists/*

# mono
RUN apt-get update -qq && \
  apt-get upgrade -qqy && \
  apt-get install -qqy --no-install-recommends mono-complete monodevelop monodevelop-nunit nunit-console && \
  rm -rf /var/lib/apt/lists/*
ENV MONO_PATH /usr/lib/monodevelop/AddIns/NUnit