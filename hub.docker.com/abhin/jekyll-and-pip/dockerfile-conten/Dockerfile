FROM 42nerds/ant:latest
MAINTAINER 42nerds - Inh. Julian Kaffke <info@42nerds.com>

RUN dpkg --add-architecture i386 && \
    apt-get update -y && \
    apt-get install -y libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1 && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoremove -y && \
    apt-get clean

ENV ANDROID_VERSIONS android-18,android-19,android-20,android-21,android-22
ENV ANDROID_BUILD_TOOLS 22.0.1
ENV ANDROID_HOME /opt/android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools
ENV ANDROID_FILE android-sdk_r24.4.1-linux.tgz

RUN cd /opt && wget -q http://dl.google.com/android/${ANDROID_FILE} && \
    tar xzf ${ANDROID_FILE} && \
    echo y | android update sdk -u -a --filter tools,platform-tools,${ANDROID_VERSIONS},build-tools-${ANDROID_BUILD_TOOLS} && \
    rm ${ANDROID_FILE} 