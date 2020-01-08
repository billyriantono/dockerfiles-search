FROM ubuntu:18.04
MAINTAINER Steyn Geldenhuys "steyn@truevolve.technology"

USER root
RUN dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get install -y sudo git software-properties-common wine64 libgtk-3-dev gtk2-engines libxtst6 libxxf86vm1 freeglut3 libxslt1.1 libcanberra-gtk-module libxext-dev libxrender-dev libxtst-dev* x11-apps git unzip && \
    apt-get clean && apt-get purge && apt-get autoremove

COPY zulu11.31.11-ca-jdk11.0.3-linux_x64.tar.gz /tmp/zulu-11-amd64.tar.gz
RUN mkdir -p /usr/lib/jvm/zulu-11-amd64 && \
    tar xfvz /tmp/zulu-11-amd64.tar.gz --directory /usr/lib/jvm/zulu-11-amd64 --strip-components 1 && \
    sh -c 'for bin in /usr/lib/jvm/zulu-11-amd64/bin/*; do update-alternatives --install /usr/bin/$(basename $bin) $(basename $bin) $bin 100; done' && \
    sh -c 'for bin in /usr/lib/jvm/zulu-11-amd64/bin/*; do update-alternatives --set $(basename $bin) $bin; done'

COPY zulu11.1.8-ca-jdk11-c2-linux_aarch32hf.tar.gz /tmp/zulu-11-aarch32hf.tar.gz
RUN mkdir -p /usr/lib/jvm/zulu-11-aarch32hf && \
    tar xfvz /tmp/zulu-11-aarch32hf.tar.gz --directory /usr/lib/jvm/zulu-11-aarch32hf --strip-components 1

COPY openjfx-11.0.2_linux-x64_bin-sdk.zip /tmp/openjfx-11-amd64.zip
RUN mkdir -p /home/developer/openjfx-11 && \
    unzip -d /home/developer/openjfx-11 /tmp/openjfx-11-amd64.zip

COPY openjfx-11.0.2_armv6hf_bin-sdk.zip /tmp/openjfx-11-amd64.zip
RUN mkdir -p /home/developer/openjfx-11 && \
    unzip -d /home/developer/openjfx-11 /tmp/openjfx-11-amd64.zip
    
RUN mkdir -p /home/developer/ && \
    echo "developer:x:1000:1000:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:1000:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    adduser developer video && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown developer:developer -R /home/developer

USER developer

COPY wine64 /home/developer/wine64

ENV GRADLE_FOLDER /home/developer/.gradle
RUN mkdir ${GRADLE_FOLDER}
RUN echo "allprojects {\n    repositories {\n        mavenLocal()\n            maven {\n	        credentials {\n	            username travenUser\n	            password travenPassword\n\
            }\n            url \"https://truevolve-traven.appspot.com\"\n        }\n    }\n}\n" > ${GRADLE_FOLDER}/init.gradle

RUN echo "travenUser=REPLACE_THIS_WITH_YOUR_USERNAME\ntravenPassword=REPLACE_THIS_WITH_YOUR_PASSWORD\norg.gradle.caching=true" > ${GRADLE_FOLDER}/gradle.properties
RUN sudo chmod -R 0777 /home/developer/wine64/ && \
    sudo chown developer:developer -R /home/developer
     
ENV JAVA_HOME /usr/lib/jvm/zulu-11-amd64
ENV HOME /home/developer
WORKDIR /home/developer
