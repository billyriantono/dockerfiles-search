############################################################
# Dockerfile to build jenkins swarm slaves container images that can build and publish new unity projects
# Based on ubuntu
############################################################

FROM ubuntu
MAINTAINER Holger Zunker <holger50@gmx.de>

# Create a non-root user
RUN useradd -m user
USER root

 

RUN dpkg --add-architecture i386 && apt-get -qq update && DEBIAN_FRONTEND=noninteractive apt-get -qq install -y \
      expect \
      xvfb \
      curl \
      gconf-service \
      lib32gcc1 lib32stdc++6 xz-utils libasound2 libc6 libc6-i386 libcairo2 libcap2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libfreetype6 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libgl1-mesa-glx libglib2.0-0 libglu1-mesa libgtk2.0-0 libgtk-3-0 libnspr4 libnss3 libpango1.0-0 libstdc++6 libx11-6 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxtst6 zlib1g debconf npm libsoup2.4-1 \
      libarchive13 \
      wget \
      openjdk-8-jdk \
      git-core \
      xz-utils \
      unzip \
    && apt-get -y upgrade \
    && rm -rf /var/lib/apt/lists/*

USER root
ENV UNITY_VERSION="2018.3.2f1"
RUN wget https://beta.unity3d.com/download/b3c100a4b73a/UnitySetup-${UNITY_VERSION} -O UnitySetup
# make executable
RUN chmod +x UnitySetup && \
    # install unity with required components. Show available components in log
    ./UnitySetup --list-components && \
    # agree with license
    echo y | \
    ./UnitySetup --unattended --install-location=/opt/Unity/Editor --verbose --download-location=/tmp/unity --components=Unity,Android,WebGL,Windows-Mono && \
    # remove setup
    rm UnitySetup && \
    # make a directory for the certificate Unity needs to run
    mkdir -p $HOME/.local/share/unity3d/Certificates/

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64

USER user

# Install Android tools
# Download Android SDK
ENV BUILD_TOOLS_VERSION 28.0.3
ENV ANDROID_VERSION 26
ENV SDK_VERSION="sdk-tools-linux-3859397.zip"
ENV ANDROID_HOME="/home/user/android-sdk-linux"
ENV ANDROID_NDK /home/user/android-ndk-linux
ENV ANDROID_NDK_HOME /home/user/android-ndk-linux
ENV SDK_URL="https://dl.google.com/android/repository/{$SDK_VERSION}"
ENV PATH="/home/user/gradle/bin:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/tools/bin:${PATH}"
USER root
RUN mkdir -p "$ANDROID_HOME" && cd "$ANDROID_HOME"
RUN curl -o tools-sdk.zip https://dl.google.com/android/repository/$SDK_VERSION && \
    unzip tools-sdk.zip -d $ANDROID_HOME/ && \
    rm -f tools-sdk.zip
    
RUN cd /home/user && \
    wget -q --output-document=android-ndk.zip https://dl.google.com/android/repository/android-ndk-r18b-linux-x86_64.zip && \
	unzip android-ndk.zip && \
	rm -f android-ndk.zip && \
	mv android-ndk-r18b android-ndk-linux

RUN chmod -R 755 $ANDROID_HOME/* && chown -R user:user $ANDROID_HOME/*
COPY licenses /home/user/android-sdk-linux/licenses
COPY scripts/android-accept-licenses.sh /home/user/scripts/
RUN chmod 755 /home/user/scripts/*
RUN /home/user/scripts/android-accept-licenses.sh "$ANDROID_HOME/tools/bin/sdkmanager platform-tools \"build-tools;${BUILD_TOOLS_VERSION}\" \"platforms;android-${ANDROID_VERSION}\" \"add-ons;addon-google_apis-google-24\" \"extras;m2repository;com;android;support;constraint;constraint-layout;1.0.2\" \"extras;m2repository;com;android;support;constraint;constraint-layout-solver;1.0.2\" \"system-images;android-${ANDROID_VERSION};google_apis;armeabi-v7a\" ndk-bundle"


#Install Jenkins dependencies
ENV JENKINS_MASTER_USERNAME="jenkins" \
    JENKINS_MASTER_PASSWORD="jenkins" \
    JENKINS_MASTER_URL="http://jenkins:8080/" \
    JENKINS_SLAVE_MODE="exclusive" \
    JENKINS_SLAVE_NAME="Unity-${UNITY_VERSION}" \
    JENKINS_SLAVE_WORKERS="1" \
    JENKINS_SLAVE_LABELS="unity unity-${UNITY_VERSION} Java Java8 java java8" \
    AVD=""
ENV JENKINS_SLAVE_ROOT="/home/user/"
ENV HOME=/home/user \
    JENKINS_SWARM_VERSION=3.15 \
    JENKINS_SWARM_JAR_PATH=/home/user
ENV JENKINS_SWARM_JAR=${JENKINS_SWARM_JAR_PATH}/swarm.jar
RUN mkdir -p "$JENKINS_SLAVE_ROOT"
# Install Jenkins slave (swarm)
RUN mkdir -p $JENKINS_SWARM_JAR_PATH \
    && chmod 755 $JENKINS_SWARM_JAR_PATH \
    && curl -SLo $JENKINS_SWARM_JAR http://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/$JENKINS_SWARM_VERSION/swarm-client-$JENKINS_SWARM_VERSION.jar

ENV DISPLAY=:0

#USER root
#RUN env | grep -E "(JENKINS|JAVA)" > /etc/docker.properties

USER user
COPY scripts/entrypoint.sh /home/user/scripts/
COPY scripts/Unity_lic.ulf /home/user/.local/share/unity3d/Unity/Unity_lic.ulf

USER root
RUN chmod 755 /home/user/scripts/entrypoint.sh
RUN chmod 755 -R /home/user/.local/share/* && chown user:user -R /home/user/.local/share

RUN mkdir -p /home/user/.cache/unity3d/Unity && \
    chmod 755 -R /home/user/.cache/unity3d && \
    chown user:user -R /home/user/.cache/unity3d && \
    mkdir -p /home/user/.android && \
    touch /home/user/.android/repositories.cfg && \
    chmod 755 -R /home/user/.android/ && \
    chown user:user -R /home/user/.android/


USER user
ENTRYPOINT ["/home/user/scripts/entrypoint.sh"]
CMD ["bash"]
VOLUME ${HOME}
WORKDIR ${HOME}
