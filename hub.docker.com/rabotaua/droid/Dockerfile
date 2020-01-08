FROM ubuntu

RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository ppa:webupd8team/java -y
RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections
RUN apt-get update && apt-get install -y oracle-java8-installer maven wget unzip curl zip python3

# https://developer.android.com/studio/#downloads
RUN wget https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip
RUN unzip sdk-tools-linux-4333796.zip
RUN rm sdk-tools-linux-4333796.zip
RUN mkdir android-sdk
RUN mv tools android-sdk/tools

ENV ANDROID_HOME=/android-sdk
ENV PATH=$PATH:$ANDROID_HOME/tools/bin
ENV PATH=$PATH:$ANDROID_HOME/platform-tools


RUN yes | sdkmanager --licenses
