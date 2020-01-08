FROM travix/base-debian-jre8

# intall the java dependencies (JDK, Maven, Ant)
RUN echo "deb http://http.debian.net/debian jessie-backports main" | tee /etc/apt/sources.list.d/jessie-backports.list \
  && apt-get update \
  && apt-get install -y --no-install-recommends -t jessie-backports \
    openjdk-8-jdk-headless \
    openjdk-8-jdk \
    maven \
  && apt-get install -y --no-install-recommends \
    ant \
    libgconf-2-4 \
    libqt5widgets5

# install the android SDK
ENV ANDROID_SDK_VERSION="r24.4.1" \
  ANDROID_API_LEVEL="android-22" \
  ANDROID_BUILD_TOOLS_VERSION="22.0.1" \
  ANDROID_DEVICE_ABI="armeabi-v7a"

RUN curl -fSL "https://dl.google.com/android/repository/tools_${ANDROID_SDK_VERSION}-linux.zip" -o android.zip \
  && mkdir /root/.android \
  && unzip android.zip -d /root/.android \
  && rm -rf android.zip

ENV ANDROID_HOME="/root/.android" \
  PATH=$PATH:/root/.android/tools:/root/.android/platform-tools:/root/.android/tools/bin


RUN echo "y" | android update sdk --no-ui --all --force --filter platform-tools,${ANDROID_API_LEVEL},sys-img-${ANDROID_DEVICE_ABI}-${ANDROID_API_LEVEL},build-tools-${ANDROID_BUILD_TOOLS_VERSION} \
  && echo "y" | android update adb

# install NodeJS
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash - \
  && apt-get update \
  && apt-get install -y --no-install-recommends nodejs \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# install Appium
RUN npm install -g \
  gulp \
  appium@1.6.3 --chromedriver_version="2.16"

# AVD/Selenium related configuration
ENV ANDROID_DEVICE_TYPE="14" \
  ANDROID_DEVICE_NAME="Nexus" \
  ANDROID_DEVICE_SKIN="WVGA800" \
  HUB_PORT_4444_TCP_PORT="4444" \
  HUB_PORT_4444_TCP_ADDR="127.0.0.1" \
  DBUS_SESSION_BUS_ADDRESS="/dev/null"

# import configuration for the Selenium Grid
COPY config.sh /opt

ENTRYPOINT ["/opt/config.sh"]

EXPOSE 8000 4723 2252 4444

# start the node
CMD emulator64-arm -verbose -avd ${ANDROID_DEVICE_NAME} -no-boot-anim -no-window -noaudio -gpu off & (adb wait-for-device && appium --nodeconfig /opt/config.json)
