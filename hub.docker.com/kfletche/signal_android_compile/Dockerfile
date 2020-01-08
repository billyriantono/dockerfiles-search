FROM ubuntu:14.04

RUN dpkg --add-architecture i386 && \
    apt-get update -y && \
    apt-get install -y git software-properties-common libgl1-mesa-dev:i386 libncurses5:i386 libstdc++6:i386 zlib1g:i386 && \
    add-apt-repository ppa:webupd8team/java && \
    apt-get update -y && \
    echo y | apt-get install -y oracle-java7-installer 
#    apt-get install -y openjdk-7-jdk  

ADD http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz /tmp/

RUN tar -xzf /tmp/android-sdk_r24.4.1-linux.tgz -C /tmp && \
    mv /tmp/android-sdk-linux /usr/local/ && \
    rm -f /tmp/android-sdk_r24.4.1-linux.tgz

RUN echo 'export PATH=${PATH}:/usr/local/android-sdk-linux/tools:/usr/local/android-sdk-linux/tools' >> .bashrc
ENV PATH /usr/local/android-sdk-linux/tools:/usr/local/android-sdk-linux/tools:$PATH

RUN mkdir /src
WORKDIR /src

RUN git clone https://github.com/WhisperSystems/Signal-Android.git .

RUN echo 'sdk.dir=/usr/local/android-sdk-linux/' >> local.properties

RUN android list sdk --all --extended

RUN FILTER=platform-tools,extra-google-google_play_services,build-tools-22.0.1,android-22,extra-android-m2repository,extra-google-m2repository && \
    ( sleep 5 && while [ 1 ]; do sleep 1; echo y; done ) \
       | android update sdk --no-ui --all \
       --filter ${FILTER}

RUN ./gradlew build 

# Entrypoint
CMD /bin/bash
