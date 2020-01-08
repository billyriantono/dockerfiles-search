FROM ubuntu:14.04
MAINTAINER Ryan Fowler <rwfowler@gmail.com>

RUN apt-get -y update
RUN apt-get install -y --no-install-recommends openjdk-7-jdk
RUN apt-get install -y curl
RUN useradd --create-home jenkins
USER jenkins
WORKDIR /home/jenkins
ADD ./start /start
CMD /start
