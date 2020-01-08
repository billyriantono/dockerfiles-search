FROM java:8

RUN apt-get update \
    && apt-get -y install file build-essential

ENV SDK_URL             https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip
ENV ANDROID_HOME        /usr/local/android-sdk
ENV ANDROID_NDK_HOME    $ANDROID_HOME/ndk-bundle
ENV PATH                $ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_NDK_HOME:$PATH

# download and unzip sdk
RUN mkdir -p $ANDROID_HOME \ 
    && wget -q $SDK_URL -O android-sdk.zip \
    && unzip android-sdk.zip -d $ANDROID_HOME \
    && rm -f android-sdk.zip

RUN mkdir $HOME/.android
RUN echo 'count=0' > $HOME/.android/repositories.cfg

# Accept licenses before installing components
RUN yes | sdkmanager --licenses

# Platform tools
RUN sdkmanager "platform-tools"

# SDKs
# The `yes` is for accepting all non-standard tool licenses.
RUN yes | sdkmanager \ 
    "platforms;android-27" \
    "build-tools;27.0.3"

# NDK
RUN sdkmanager "ndk-bundle"
