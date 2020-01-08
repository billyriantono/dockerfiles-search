FROM openjdk:8-jdk

ENV ANDROID_HOME /opt/android-sdk-linux
ENV ANDROID_SDK_ROOT $ANDROID_HOME
ENV ANDROID_SDK_TOOLS_VERSION 4333796
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LANGUAGE en_US:en
ENV FLUTTER_HOME ${HOME}/sdks/flutter
ENV FLUTTER_ROOT $FLUTTER_HOME
ENV FLUTTER_VERSION v1.7.8+hotfix.3
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools:

RUN apt-get -o Acquire::http::Pipeline-Depth=0 -o Acquire::http::No-Cache=true -o Acquire::BrokenProxy=true update
RUN  apt-get -o Acquire::http::Pipeline-Depth=0 -o Acquire::http::No-Cache=true -o Acquire::BrokenProxy=true install -yq --allow-unauthenticated --no-install-recommends lib32stdc++6 locales bash curl git unzip xz-utils libglu1-mesa software-properties-common build-essential lib32stdc++6 sudo lib32stdc++6 libstdc++6 lcov

RUN cd /opt
RUN wget -q https://dl.google.com/android/repository/sdk-tools-linux-$ANDROID_SDK_TOOLS_VERSION.zip -O android-sdk-tools.zip
RUN unzip -q android-sdk-tools.zip -d ${ANDROID_HOME}
RUN rm android-sdk-tools.zip

RUN yes | sdkmanager --licenses

RUN touch /root/.android/repositories.cfg
RUN sdkmanager tools
RUN sdkmanager platform-tools
RUN sdkmanager emulator

RUN sh -c 'echo "en_US.UTF-8 UTF-8" > /etc/locale.gen'
RUN locale-gen
RUN update-locale LANG=en_US.UTF-8

RUN mkdir -p $FLUTTER_HOME
RUN cd /tmp/
RUN wget -O flutter.tar.xz https://storage.googleapis.com/flutter_infra/releases/stable/linux/flutter_linux_${FLUTTER_VERSION}-stable.tar.xz
RUN tar xf flutter.tar.xz --strip-components=1 -C ${FLUTTER_HOME}
RUN ls -la ${FLUTTER_HOME}/

ENV PATH ${PATH}:${FLUTTER_HOME}/bin:${FLUTTER_HOME}/bin/cache/dart-sdk/bin

RUN flutter config --no-analytics
RUN flutter precache
RUN flutter doctor
RUN flutter --version
