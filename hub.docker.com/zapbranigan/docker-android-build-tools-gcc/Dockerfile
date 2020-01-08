from ubuntu

maintainer Alexey Kuznetsov <kuznetsovalexey34@gmail.com>

run apt-get update

run apt-get -y upgrade

run apt-get install -y unzip

run apt-get install -y wget

run apt-get install -y openjdk-8-jdk

run apt-get install -y git

run apt-get install -y openssh-client

run wget -O /tmp/z.$$ https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip

run unzip -d /usr/lib/android-sdk /tmp/z.$$

run rm /tmp/z.$$

run yes|/usr/lib/android-sdk/tools/bin/sdkmanager --licenses 

run yes|/usr/lib/android-sdk/tools/bin/sdkmanager --update

run yes|/usr/lib/android-sdk/tools/bin/sdkmanager ndk-bundle

run apt-get install -y openssh-client

RUN apt-get install -y locales

RUN locale-gen en_US.UTF-8

ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'

run apt-get install -y build-essential

run apt-get install -y curl

env ANDROID_HOME /usr/lib/android-sdk

copy root_pem_geotrust_rapidssl.crt /usr/local/share/ca-certificates/

copy intermediate_pem_geotrust_rapidssl.crt /usr/local/share/ca-certificates/

run update-ca-certificates --fresh

RUN useradd -ms /bin/bash jenkins

#Cleaning

RUN apt-get clean

RUN apt-get autoclean

RUN apt-get autoremove
