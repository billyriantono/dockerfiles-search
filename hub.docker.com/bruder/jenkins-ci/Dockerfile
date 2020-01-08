FROM jenkins:latest

MAINTAINER  Mike Bruder it.bruder@gmail.com

USER root

RUN apt-get update -qq && apt-get install -qqy wget

RUN wget http://www.dotdeb.org/dotdeb.gpg
RUN apt-key add dotdeb.gpg
RUN rm -rf dotdeb.gpg

RUN echo "deb http://ftp.de.debian.org/debian/ buster main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb-src http://ftp.de.debian.org/debian/ buster main contrib non-free" >> /etc/apt/sources.list

RUN apt-get update -qq && \
    apt-get install -qqy --no-install-recommends apt-utils && \
    apt-get install -qqy --no-install-recommends doxygen && \
    apt-get install -qqy doxygen-doc graphviz && \

    apt-get -t testing install -qqy astyle && \

    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

USER jenkins
