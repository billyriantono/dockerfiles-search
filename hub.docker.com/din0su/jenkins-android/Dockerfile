FROM jenkins

# Android SDK
#RUN wget --progress=dot:giga https://dl.google.com/android/android-sdk_r24.4.1-linux.tgz
VOLUME /opt/android-sdk
#RUN mv android-sdk_r24.4.1-linux.tgz /opt/
#RUN cd /opt && tar xzf android-sdk_r24.4.1-linux.tgz
#RUN cd /opt && rm -f android-sdk_r22.6-linux.tgz
#
# Other tools and resources of Android SDK
ENV ANDROID_HOME /opt/android-sdk
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools
#RUN echo y | android update sdk --filter platform-tools,build-tools-19.0.3,android-17,extra-android-support --no-ui --force
