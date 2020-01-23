FROM abiskop/base

RUN echo deb http://archive.ubuntu.com/ubuntu precise main universe > /etc/apt/sources.list
RUN echo deb http://archive.ubuntu.com/ubuntu precise-updates main universe >> /etc/apt/sources.list
RUN apt-get update
RUN apt-get upgrade -y --no-install-recommends

RUN apt-get install -y openjdk-7-jdk --no-install-recommends
RUN java -version

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

