FROM ubuntu:17.04



RUN apt-get update && apt-get install -y curl apt-transport-https && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y yarn

RUN curl -sL https://deb.nodesource.com/setup_7.x | bash -

RUN apt-get update
RUN apt-get -y install openjdk-8-jdk
RUN apt-get -y install virtualbox
RUN apt-get -y install nodejs
RUN apt-get -y install virtualbox-dkms
RUN apt-get install linux-headers-generic
RUN dpkg-reconfigure virtualbox-dkms
RUN apt-get -y install wget

RUN wget https://files.boxfuse.com/com/boxfuse/client/boxfuse-commandline/1.26.1.1297/boxfuse-commandline-1.26.1.1297-linux-x64.tar.gz
RUN tar -zxvf boxfuse-commandline-1.26.1.1297-linux-x64.tar.gz
WORKDIR ./boxfuse
ENV PATH "$PATH:/boxfuse"