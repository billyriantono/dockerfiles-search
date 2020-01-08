FROM swun9/docker-ubuntu-java:latest
MAINTAINER swun9 "swung.cn@gmail.com"
ENV REFRESHED_AT 2015-01-11

RUN apt-get -qq update 
RUN apt-get -qqy install libstdc++6 lib32z1 lib32stdc++6 expect
RUN apt-get -qqy install bison g++-multilib git gperf libxml2-utils
 
# Android config
RUN curl -L https://raw.githubusercontent.com/swung/android-sdk-installer/master/android-sdk-installer | bash /dev/stdin --install=tools,platform-tools,build-tools-20.0.0,build-tools-19.1.0,build-tools-19.0.3,android-L,android-20,android-19,sysimg-19,extra-android-support,extra-android-m2repository --dir=/opt --accept="android-sdk-license-5be876d5|android-sdk-preview-license-52d11cd2"
RUN rm /opt/android-sdk*linux.tgz
ENV ["ANDROID_HOME", "/opt/android-sdk-linux"]
