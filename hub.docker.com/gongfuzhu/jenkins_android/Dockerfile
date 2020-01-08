FROM jenkins/jenkins:lts
USER root

RUN apt-get update

ENV ANDROID_HOME=/var/android-sdk

RUN cd /var \
	&& curl -O https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip \
	&& unzip -d ${ANDROID_HOME} sdk-tools-linux-4333796.zip
	
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools

RUN yes | sdkmanager  --licenses
RUN touch /root/.android/repositories.cfg
RUN sdkmanager "emulator" "tools" "platform-tools"
RUN yes | sdkmanager --update --channel=3
#RUN yes | sdkmanager \
#    "platforms;android-29" \
#    "platforms;android-28" \
#    "platforms;android-27" \
#    "platforms;android-26" \
#    "platforms;android-25" \
#    "platforms;android-24" \
#    "platforms;android-23" \
#    "platforms;android-22" \
#    "platforms;android-21" \
#    "platforms;android-19" \
#    "platforms;android-17" \
#    "platforms;android-15" \
#    "build-tools;29.0.2" \
#    "build-tools;29.0.1" \
#    "build-tools;29.0.0" \
#    "build-tools;28.0.3" \
#    "build-tools;28.0.2" \
#    "build-tools;28.0.1" \
#    "build-tools;28.0.0" \
#    "build-tools;27.0.3" \
#    "build-tools;27.0.2" \
#    "build-tools;27.0.1" \
#    "build-tools;27.0.0" \
#    "build-tools;26.0.2" \
#    "build-tools;26.0.1" \
#    "build-tools;25.0.3" \
#    "build-tools;24.0.3" \
#    "build-tools;23.0.3" \
#    "build-tools;22.0.1" \
#    "build-tools;21.1.2" \
#    "build-tools;19.1.0" \
#    "build-tools;17.0.0" \
#    "system-images;android-29;google_apis;x86" \
#    "system-images;android-28;google_apis;x86" \
#    "system-images;android-26;google_apis;x86" \
#    "system-images;android-25;google_apis;armeabi-v7a" \
#    "system-images;android-24;default;armeabi-v7a" \
#    "system-images;android-22;default;armeabi-v7a" \
#    "system-images;android-19;default;armeabi-v7a" \
#    "extras;android;m2repository" \
#    "extras;google;m2repository" \
#    "extras;google;google_play_services" \
#    "extras;m2repository;com;android;support;constraint;constraint-layout;1.0.2" \
#    "extras;m2repository;com;android;support;constraint;constraint-layout;1.0.1" \
#    "add-ons;addon-google_apis-google-23" \
#    "add-ons;addon-google_apis-google-22" \
#    "add-ons;addon-google_apis-google-21"
USER jenkins
