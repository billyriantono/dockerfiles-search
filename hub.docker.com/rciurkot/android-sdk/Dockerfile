FROM ubuntu:17.04

MAINTAINER Rafał Ciurkot <rafal.ciurkot@workhq.com>

# Install java8
RUN apt-get update && apt-get install -y \
    unzip \
    software-properties-common \
    wget; \
    echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections; \
    add-apt-repository -y ppa:webupd8team/java; \
    apt-get update && apt-get install -y \
    oracle-java8-installer; \
    apt-get autoremove && apt-get clean && rm -rf /var/lib/apt/lists/*

# Setup environment
ENV ANDROID_HOME /opt/android-sdk

WORKDIR ${ANDROID_HOME}

# Install Android SDK
RUN wget --output-document=android-sdk.zip https://dl.google.com/android/repository/tools_r25.2.3-linux.zip; \
    unzip android-sdk.zip && rm -f android-sdk.zip
ENV PATH ${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin::${ANDROID_HOME}/platform-tools:${PATH}
COPY .android/ /root/.android
RUN mkdir "$ANDROID_HOME/licenses"
RUN echo -e "\n8933bad161af4178b1185d1a37fbf41ea5269c55" > "$ANDROID_HOME/licenses/android-sdk-license" \
    echo -e "\n84831b9409646a918e30573bab4c9c91346d8abd" > "$ANDROID_HOME/licenses/android-sdk-preview-license" \
    echo -e "\nd975f751698a77b662f1254ddbeed3901e976f5a" > "$ANDROID_HOME/licenses/intel-android-extra-license"

# Install Android dependencies
RUN echo y | sdkmanager --update
RUN	sdkmanager "extras;android;m2repository" "extras;google;m2repository" 


# cd to workspace
WORKDIR /root/workspace
