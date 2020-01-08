FROM sergey11166/android-sdk-gcloud-docker

ENV ANDROID_NDK=/opt/android-ndk-linux
ENV ANDROID_NDK_HOME=/opt/android-ndk-linux
ENV NDK_ZIP_FILE=android-ndk-r18-linux-x86_64.zip

ADD https://dl.google.com/android/repository/${NDK_ZIP_FILE} /opt
RUN cd /opt && unzip ${NDK_ZIP_FILE} && rm -f ${NDK_ZIP_FILE} && mv android-ndk-r18 android-ndk-linux
