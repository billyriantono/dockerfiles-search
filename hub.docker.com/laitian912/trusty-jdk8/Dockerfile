FROM evarga/jenkins-slave
MAINTAINER Tian Lai <laitian912@gmail.com>

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get remove -y openjdk-7-jre-headless

RUN apt-get install -y  \
    git                 \
    curl                \
    software-properties-common

RUN add-apt-repository -y ppa:openjdk-r/ppa
RUN apt-get update
RUN apt-get install -y openjdk-8-jdk

RUN curl -fsSL https://get.docker.com/ | sh

ENV TZ=America/Los_Angeles
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
