FROM ubuntu:18.04
MAINTAINER Steyn Geldenhuys "steyn@truevolve.technology"

USER root
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
    apt-get dist-upgrade -y && \
    apt-get install -y qemu-kvm libvirt-bin curl unzip lib32z1 lib32ncurses5 lib32stdc++6 git vim ant libc6-i386 sudo make libglu1-mesa firefox \
                       ffmpeg libsdl2-2.0.0 make gcc pkg-config meson libavcodec-dev libavformat-dev libavutil-dev libsdl2-dev openjdk-8-jdk && \
    apt-get clean && apt-get purge

RUN mkdir -p /home/developer/ && \
    echo "developer:x:1000:1000:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:1000:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    adduser developer kvm && \
    adduser developer video && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown developer:developer -R /home/developer

USER developer
RUN curl https://dl.google.com/dl/android/studio/ide-zips/3.5.2.0/android-studio-ide-191.5977832-linux.tar.gz -o /home/developer/android-studio.tar.gz

RUN  mkdir /home/developer/android-studio && \
     tar -xvzf /home/developer/android-studio.tar.gz -C /home/developer/android-studio --strip-components 1 && \
     rm /home/developer/android-studio.tar.gz && \
     chmod +x /home/developer/android-studio/bin/studio.sh

USER developer
ENV HOME /home/developer
ENV ANDROID_HOME=/home/developer/Android/Sdk
ENV PATH=$PATH:$ANDROID_HOME/platform-tools/
WORKDIR /home/developer
CMD cd /home/developer/android-studio/bin/ && ./studio.sh
