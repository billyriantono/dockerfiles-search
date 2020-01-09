FROM library/debian:wheezy
MAINTAINER rgranadosd@gmail.com
RUN apt-get -y update &&\
    apt-get -y upgrade &&\
    apt-get install -y man funny-manpages
ENTRYPOINT ["/usr/bin/man"]
