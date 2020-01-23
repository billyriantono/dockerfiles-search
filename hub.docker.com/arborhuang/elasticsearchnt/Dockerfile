FROM arabella/node-yarn-zsh-local


# ——————————
# Install Java 8
# ——————————

RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" > /etc/apt/sources.list.d/webupd8team-java.list && \
  echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" >> /etc/apt/sources.list.d/webupd8team-java.list && \
  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886 && \
  apt-get update && \
  apt-get install oracle-java8-installer -y && \
  rm -rf /var/lib/apt/lists/* && \
  apt-get autoremove -y && \
  apt-get clean

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle


# ——————————
# Install i386 architecture required for running 32 bit Android tools
# ——————————

RUN dpkg --add-architecture i386 && \
  apt-get update -y && \
  apt-get install -y libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1 && \
  rm -rf /var/lib/apt/lists/* && \
  apt-get autoremove -y && \
  apt-get clean


# ——————————
# Install Android SDK
# ——————————

ENV ANDROID_SDK_VERSION r24.4.1
ENV ANDROID_BUILD_TOOLS_VERSION build-tools-23.0.3,build-tools-23.0.2,build-tools-23.0.1

ENV ANDROID_SDK_FILENAME android-sdk_${ANDROID_SDK_VERSION}-linux.tgz
ENV ANDROID_SDK_URL http://dl.google.com/android/${ANDROID_SDK_FILENAME}
ENV ANDROID_API_LEVELS android-23
ENV ANDROID_EXTRA_COMPONENTS extra-android-m2repository,extra-google-m2repository,extra-android-support,extra-google-google_play_services
ENV ANDROID_HOME /opt/android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools
RUN cd /opt && \
  wget -q ${ANDROID_SDK_URL} && \
  tar -xzf ${ANDROID_SDK_FILENAME} && \
  rm ${ANDROID_SDK_FILENAME} && \
  echo y | android update sdk --no-ui -a --filter tools,platform-tools,${ANDROID_API_LEVELS},${ANDROID_BUILD_TOOLS_VERSION} && \
  echo y | android update sdk --no-ui --all --filter "${ANDROID_EXTRA_COMPONENTS}"

# udev rules for most android devices
RUN cd /etc/udev/rules.d/ && \
  wget https://raw.githubusercontent.com/M0Rf30/android-udev-rules/master/51-android.rules
