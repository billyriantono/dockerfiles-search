## Write by SangSoo kim <sskim.luis@gmail.com>
## ex) docker build --rm --build-arg USER=$USER --build-arg UID=`id -u` --tag jeju_android:1.0 .

FROM ubuntu:14.04

ARG USER
ENV USER ${USER:-luis}

ARG UID
ENV UID ${UID:-1000}

RUN apt-get update
RUN apt-get install -qq software-properties-common tzdata

# Set timezone to "Asia/Seoul"
ENV TZ=Asia/Seoul
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install JDK
RUN add-apt-repository ppa:openjdk-r/ppa  
RUN apt-get update
RUN apt-get install -qq openjdk-8-jre openjdk-8-jdk

# Install for android build packages
RUN apt-get install -qq git-core gnupg flex bison gperf build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip ruby libssl-dev
RUN apt-get install -qq bc m4 wget

# Install Python
RUN apt-get install -qq python2.7
RUN ln -s /usr/bin/python2.7 /usr/bin/python

# Remove cached files
RUN rm -rf /var/lib/apt/lists/*
RUN apt-get autoclean
RUN apt-get autoremove
RUN apt-get clean

# Add user for $USER
RUN useradd -m $USER -s /bin/bash -u $UID && echo $USER:$USER | chpasswd && adduser $USER sudo
USER $USER
