FROM ubuntu
MAINTAINER mwaeckerlin

ENV CREATE ""

RUN apt-get update
RUN apt-get install -y subversion

ADD start.sh /start.sh
CMD /start.sh

VOLUME /svn
