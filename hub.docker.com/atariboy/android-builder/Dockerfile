FROM philcryer/min-wheezy:latest

MAINTAINER Andy Lee "xatariboyx@gmail.com"

RUN dpkg --add-architecture i386 && apt-get update && apt-get install -y --force-yes expect git wget libc6-i386 lib32stdc++6 lib32gcc1 lib32ncurses5 lib32z1 python curl && apt-get clean && rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/*
 
RUN echo "deb http://httpredir.debian.org/debian jessie main" | tee /etc/apt/sources.list.d/jessie.list
RUN apt-get update && apt-get install -y --force-yes webp && apt-get clean && rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install java8
RUN apt-get update && apt-get install -y software-properties-common && apt-get clean && rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu yakkety main" | tee /etc/apt/sources.list.d/webupd8team-java.list
RUN echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu yakkety main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886
RUN apt-get update && echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && apt-get install -y oracle-java8-installer && apt-get clean && rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install stuff
RUN echo "deb http://ppa.launchpad.net/cwchien/gradle/ubuntu yakkety main" | tee /etc/apt/sources.list.d/gradle.list
RUN apt-get update && apt-get install -y --force-yes make gradle imagemagick python && ln -s /usr/bin/convert /usr/bin/convert_img

RUN echo "deb http://httpredir.debian.org/debian jessie main" | tee /etc/apt/sources.list.d/jessie.list
RUN apt-get update && apt-get install -y --force-yes webp && apt-get clean && rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Android SDK
RUN cd /opt && wget http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz && tar -xvf android-sdk_r24.4.1-linux.tgz && rm android-sdk_r24.4.1-linux.tgz
RUN cd /opt/android-sdk-linux/tools && ( sleep 5 && while [ 1 ]; do sleep 1; echo y; done ) | ./android update sdk -u -a -t 1,3,4,5,7,8,9,12,30,31,32,108,109,110,143
ENV ANDROID_HOME /opt/android-sdk-linux

#Install Android NDK
RUN apt-get install -y unzip && cd /opt && wget http://dl.google.com/android/repository/android-ndk-r12b-linux-x86_64.zip && unzip android-ndk-r12b-linux-x86_64.zip && rm android-ndk-r12b-linux-x86_64.zip && export PATH=$PATH:/opt/android-ndk-r12b && apt-get -y remove unzip
ENV ANDROID_NDK_ROOT /opt/android-ndk-r12b
