# Android Dockerfile

FROM gradle:4.4.1-jdk-alpine

MAINTAINER Vinicius Camargo "camargo.v@gmail.com"

ENV SDK_TOOLS "24.4.1"
ENV BUILD_TOOLS "27.0.3"
ENV TARGET_SDK "27"
ENV ANDROID_HOME "/opt/android-sdk"
ENV GLIBC_VERSION "2.25-r0"
ENV ANDROID_COMPONENTS platform-tools,android-27,build-tools-27.0.3,extra-android-support,extra-google-google_play_services

USER root

# Install required dependencies
RUN apk add --no-cache --virtual=.build-dependencies wget unzip ca-certificates bash && \
    wget https://raw.githubusercontent.com/sgerrand/alpine-pkg-glibc/master/sgerrand.rsa.pub -O /etc/apk/keys/sgerrand.rsa.pub && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-${GLIBC_VERSION}.apk -O /tmp/glibc.apk && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-bin-${GLIBC_VERSION}.apk -O /tmp/glibc-bin.apk && \
    apk add --no-cache /tmp/glibc.apk /tmp/glibc-bin.apk && \
    rm -rf /tmp/* && \
    rm -rf /var/cache/apk/*

RUN apk add --no-cache git

# Download and extract Android Tools
RUN wget https://dl.google.com/android/android-sdk_r${SDK_TOOLS}-linux.tgz && \
    mkdir -p ${ANDROID_HOME} && \
    tar -xzf android-sdk_r${SDK_TOOLS}-linux.tgz && \
    mv android-sdk-linux/* ${ANDROID_HOME} && \
    rm -rf android-sdk_r${SDK_TOOLS}-linux.tgz && \
    rm -rf android-sdk-linux

# Install Android tools
RUN echo y | ${ANDROID_HOME}/tools/android update sdk --filter "${ANDROID_COMPONENTS}" --no-ui -a

# Accept Android SKD License
RUN mkdir ${ANDROID_HOME}/licenses || true && \
    echo "8933bad161af4178b1185d1a37fbf41ea5269c55" >> "${ANDROID_HOME}/licenses/android-sdk-license" && \
    echo "d56f5187479451eabf01fb78af6dfcb131a6481e" >> "${ANDROID_HOME}/licenses/android-sdk-license" && \
    echo "84831b9409646a918e30573bab4c9c91346d8abd" >> "${ANDROID_HOME}/licenses/android-sdk-preview-license"

ENV PATH $PATH:/opt/android-sdk/tools:/opt/android-sdk/platform-tools:/opt/android-sdk/build-tools/${BUILD_TOOLS}

CMD ["bash"]
