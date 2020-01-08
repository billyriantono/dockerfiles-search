FROM zzstc/jenkins-slave:base
LABEL maintainer "wulifu <kevinsocial@outlook.com>"

ENV ANDROID_SDK_URL="https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip" \
    ANDROID_BUILD_TOOLS_VERSION="28.0.3" \
    ANDROID_APIS="android-28" \
    GRADLE_HOME="/program/gradle" \
    ANDROID_HOME="/program/android" \
    GRADLE_VERSION="4.10.2"

ENV PATH="${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/build-tools/${ANDROID_BUILD_TOOLS_VERSION}:${GRADLE_HOME}/gradle-${GRADLE_VERSION}/bin"

USER root

# china sources.list
# COPY sources.list /etc/apt/sources.list

RUN apt-get update \
    # Install some system packages
    && apt-get install -y --no-install-recommends \
    build-essential \
    apt-transport-https \
    apt-utils \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get autoremove -y \
    && apt-get clean \
    # Set correct permission
    && chown -R jenkins:jenkins /home/jenkins \
    && mkdir -p /program /zzserver /zzserver/dispatch /zzserver/ws-source /zzserver/dispatch/dev /zzserver/dispatch/test /zzserver/dispatch/pre /zzserver/dispatch/prd /home/jenkins/.ssh \
    && chown -R jenkins:jenkins /zzserver \
    && chown -R jenkins:jenkins /program \
    # Install Gradle
    && mkdir -p ${GRADLE_HOME} \
    && curl -SL https://downloads.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip -o /tmp/gradle.zip \
    && unzip /tmp/gradle.zip -d /tmp/ && rm /tmp/gradle.zip \
    && mv /tmp/gradle-${GRADLE_VERSION} ${GRADLE_HOME} \    
    # Install Android SDK
    && mkdir -p ${ANDROID_HOME} && cd ${ANDROID_HOME} \
    && curl -SL ${ANDROID_SDK_URL} -o /tmp/tools.zip \
    && unzip /tmp/tools.zip -d ./ && rm /tmp/tools.zip \
    && yes | tools/bin/sdkmanager --licenses \
    && tools/bin/sdkmanager "platform-tools" "platforms;${ANDROID_APIS}" "build-tools;${ANDROID_BUILD_TOOLS_VERSION}" \
    && rm -rf /tmp/* /var/tmp/* \
    # Set Timezone to CST
    && /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" >/etc/timezone

USER jenkins
