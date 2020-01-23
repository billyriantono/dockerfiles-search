FROM ubuntu

#RUN sed -i 's/archive.ubuntu.com/ftp.nsysu.edu.tw\/Ubuntu/g' /etc/apt/sources.list
#RUN sed -i 's/archive.ubuntu/tw.archive.ubuntu/g' /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y software-properties-common

RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN apt-add-repository -y ppa:webupd8team/java
RUN apt-get install -y oracle-java8-installer
#RUN rm -rf /var/lib/apt/lists/*
RUN rm -rf /var/cache/oracle-jdk8-installer

RUN wget https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip -O sdk-tools-linux.zip

RUN apt-get install -y unzip
RUN mkdir -p /root/Android/Sdk
RUN unzip sdk-tools-linux.zip -d /root/Android/Sdk
RUN cd /root/Android/Sdk/tools/bin && ./sdkmanager --update
RUN cd /root/Android/Sdk/tools/bin && yes | ./sdkmanager --licenses
RUN cd /root/Android/Sdk/tools/bin && ./sdkmanager "platforms;android-28"
RUN cd /root/Android/Sdk/tools/bin && ./sdkmanager "build-tools;28.0.3"
RUN cd /root/Android/Sdk/tools/bin && ./sdkmanager "extras;android;m2repository"
RUN cd /root/Android/Sdk/tools/bin && ./sdkmanager "ndk-bundle"

RUN apt-get install -y curl
RUN echo "deb [arch=amd64] http://storage.googleapis.com/bazel-apt stable jdk1.8" | tee /etc/apt/sources.list.d/bazel.list
RUN curl https://bazel.build/bazel-release.pub.gpg | apt-key add -
RUN apt-get update
RUN apt-get install -y pkg-config zip g++ zlib1g-dev unzip python
RUN apt-get install -y bazel
