FROM ubuntu:xenial
MAINTAINER "Frank Wolf <FrankWolf@gmx.de>"
LABEL Maintainer="Frank Wolf <FrankWolf@gmx.de>" \
      Name="Qt for Android" \
      Version=0.1.0

RUN dpkg --add-architecture i386 && apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -qq install -y --no-install-recommends \
      ant \
      autoconf \
      autogen \
      automake \
      ca-certificates \
      curl \
      build-essential \
      dbus \
      dbus-x11 \
      expect \
      file \
      git-core \
      libglib2.0-0 \
      libtool \
      libtool-bin \
      make \
      openjdk-8-jdk \
      qt5-default \
      tightvncserver \
      unzip \
      wget \
      x11-utils \
      x11-xserver-utils \
      xfonts-base \
      libgcc1:i386 \
      libncurses5:i386 \
      libsdl1.2debian:i386 \
      libstdc++6:i386 \
      zlib1g:i386 \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

WORKDIR /opt

COPY download/ ./

# Android SDK && NDK
WORKDIR /opt/android
COPY android-accept-licenses.sh ./
ARG ANDROID_TOOLS_VERSION=25.2.5
#ARG ANDROID_NDK_VERSION=14b
#ARG ANDROID_PLATFORM_VERSION=25
#ARG ANDROID_BUILDTOOLS_VERSION=25.0.2
ARG ANDROID_NDK_VERSION=12b
ARG ANDROID_PLATFORM_VERSION=24
ARG ANDROID_BUILDTOOLS_VERSION=24.0.3

ENV ANDROID_TOOLS_URL=https://dl.google.com/android/repository/tools_r${ANDROID_TOOLS_VERSION}-linux.zip
ENV ANDROID_NDK_URL=https://dl.google.com/android/repository/android-ndk-r${ANDROID_NDK_VERSION}-linux-x86_64.zip

ENV ANDROID_HOME=/opt/android/android-sdk-linux
ENV ANDROID_NDK_ROOT=/opt/android/android-ndk
ENV PATH=${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools:${PATH}

# NDK
RUN if [ -e /opt/android-ndk-r${ANDROID_NDK_VERSION}-linux-x86_64.zip ]; then \
      mv /opt/android-ndk-r${ANDROID_NDK_VERSION}-linux-x86_64.zip . ; \
    else \
      wget -q ${ANDROID_NDK_URL}; \
    fi \
    && unzip -q android-ndk*.zip \
    && rm android-ndk*.zip \
    && ln -s android-ndk-r${ANDROID_NDK_VERSION} android-ndk \
    && if [ ! -e /opt/android/android-ndk/RELEASE.TXT ]; then \
         echo r${ANDROID_NDK_VERSION} > /opt/android/android-ndk/RELEASE.TXT ; \
       fi

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64

# SDK
RUN mkdir -p ${ANDROID_HOME} \
    && cd ${ANDROID_HOME} \
    && if [ -e /opt/tools_r${ANDROID_TOOLS_VERSION}-linux.zip ]; then \
         mv /opt/tools_r${ANDROID_TOOLS_VERSION}-linux.zip .; \
       else \
         wget -q ${ANDROID_TOOLS_URL}; \
       fi \
    && unzip -q tools*.zip \
    && rm tools*.zip \
    && echo y | ${ANDROID_HOME}/tools/bin/sdkmanager "platform-tools" \
#    && mv tools/ tools.tmp/ \
#    && echo y | ${ANDROID_HOME}/tools.tmp/bin/sdkmanager "tools" \
#    && rm -r ${ANDROID_HOME}/tools.tmp \
    && find ${ANDROID_HOME}/tools -maxdepth 1 -type f -perm 744 -print0 | xargs -0 chmod +x

# newer sdkmanager can accept all licenses with a single command
# RUN printf "y\ny\ny\ny\ny\ny\n" | ${ANDROID_HOME}/tools/bin/sdkmanager --licenses \
RUN echo y | ${ANDROID_HOME}/tools/bin/sdkmanager --include_obsolete \
      "extras;android;m2repository" \
      "extras;google;google_play_services" \
      "extras;google;m2repository" \
      "extras;google;market_apk_expansion" \
      "extras;google;market_licensing" \
      "extras;google;play_billing" \
      "extras;google;simulators" \
      "extras;google;webdriver" \
      "platforms;android-${ANDROID_PLATFORM_VERSION}" \
      "platforms;android-13" \
      "system-images;android-${ANDROID_PLATFORM_VERSION};default;armeabi-v7a" \
      "build-tools;${ANDROID_BUILDTOOLS_VERSION}"

ENV ANDROID_NDK_PLATFORM=android-9
ENV ANDROID_NDK_TOOLCHAIN_VERSION=4.9


ENV USER=root
ENV VNC_PASSWD=password

# Qt
ARG QT_VERSION=5.6.2
ENV QTDIR=/opt/Qt/5.6/android_armv7

COPY qt-installer-noninteractive.qs ./
RUN export QT_MAJOR_MINOR=$(echo $QT_VERSION | cut -d'.' -f 1,2) \
    && if [ ! -e *.run ]; then \
         if $(wget -q -S --spider https://download.qt.io/archive/qt/${QT_MAJOR_MINOR}/${QT_VERSION}/qt-opensource-linux-x64-android-${QT_VERSION}.run > /dev/null 2>&1); then \
           wget -q https://download.qt.io/archive/qt/${QT_MAJOR_MINOR}/${QT_VERSION}/qt-opensource-linux-x64-android-${QT_VERSION}.run; \
         else \
           wget -q https://download.qt.io/archive/qt/${QT_MAJOR_MINOR}/${QT_VERSION}/qt-linux-opensource-${QT_VERSION}-android-x86_64-offline.run; \
         fi \
       fi \
    && chmod +x *.run \
    && mkdir ~/.vnc \
    && printf "${VNC_PASSWD}\n${VNC_PASSWD}\nn\n" | vncpasswd \
    && tightvncserver \
    && export DISPLAY=:1 \
    && ./*.run --script qt-installer-noninteractive.qs \
    && rm *.run

# unprivileged user
ENV USER=user
ARG USER=user
ARG UID=1000
ARG GID=1000
ENV USER $USER

RUN mkdir /home/$USER \
    && groupadd -r $USER -g $GID \
    && useradd -u $UID -r -g $USER -d /home/$USER -s /usr/sbin/nologin -c "Docker User" $USER \
    && chown -R $USER:$USER /home/$USER

USER ${USER}
ADD qt.config.tgz /home/$USER/
# newer avdmanager
# RUN echo no | ${ANDROID_HOME}/tools/bin/avdmanager create avd --force --name testAVD --abi google_apis/armeabi-v7a --package 'system-images;android-${ANDROID_PLATFORM_VERSION};google_apis;armeabi-v7a'
RUN echo no | android create avd -n default-android -t 1

VOLUME /data
WORKDIR /data

CMD ["bash"]

