FROM alexpeek/gradle:4.1

LABEL maintainer="Alex Richards <alex@peekvision.org>"

ENV ANDROID_SDK_VERSION="3859397"
ENV ANDROID_SDK_LOCATION="https://dl.google.com/android/repository/sdk-tools-linux-$ANDROID_SDK_VERSION.zip" \
    ANDROID_SDK_PATH="/opt/android"
ENV ANDROID_HOME="$ANDROID_SDK_PATH/current"
ENV PATH="$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools:$PATH"

WORKDIR $ANDROID_SDK_PATH

RUN wget $ANDROID_SDK_LOCATION \
 && mkdir sdk-tools-linux-$ANDROID_SDK_VERSION \
 && unzip sdk-tools-linux-$ANDROID_SDK_VERSION.zip -d sdk-tools-linux-$ANDROID_SDK_VERSION \
 && ln -s sdk-tools-linux-$ANDROID_SDK_VERSION current \
 && mkdir -p /etc/skel/.android \
 && echo "PATH=\"$PATH\"" > /etc/skel/.profile \
 && cp /etc/skel/.profile $HOME \
 && touch /etc/skel/.android/repositories.cfg \
 && cp -R /etc/skel/.android $HOME \
 && echo -e "y\ny\ny\ny\ny\ny\ny\n" | sdkmanager --licenses \
 && sdkmanager --verbose --update
