FROM beevelop/android:latest

MAINTAINER Edson Silva <edsonluis@gmail.com>

RUN locale-gen en_US.UTF-8
ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8' \
    ANDROID_SDK_URL="https://dl.google.com/android/repository/tools_r25.2.5-linux.zip" \
    ANDROID_BUILD_TOOLS_VERSION=28.0.3 \
    ANDROID_APIS="android-10,android-15,android-16,android-17,android-18,android-19,android-20,android-21,android-22,android-23,android-24,android-25,android-26,android-27"
    
RUN apt-get update && apt-get install --no-install-recommends -y build-essential git ruby2.3-dev \
    && gem install fastlane \
    && gem install bundler \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && apt-get autoremove -y && apt-get clean

COPY android-sdk-license $ANDROID_HOME/licenses/
COPY android-sdk-preview-license $ANDROID_HOME/licenses/
