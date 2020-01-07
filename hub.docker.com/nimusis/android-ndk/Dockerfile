FROM ekreative/android:26

ENV ANDROID_NDK "ndk-bundle" "cmake;3.6.4111459" "lldb;2.3"
RUN android-accept-licenses "sdkmanager --verbose $ANDROID_NDK"
ENV ANDROID_NDK_HOME ${ANDROID_HOME}/ndk-bundle
ENV PATH ${ANDROID_NDK_HOME}:${PATH}

# toolchain error fix
# https://stackoverflow.com/questions/35128229/error-no-toolchains-found-in-the-ndk-toolchains-folder-for-abi-with-prefix-llv
RUN cd ${ANDROID_NDK_HOME}/toolchains \
    && ln -s aarch64-linux-android-4.9 mips64el-linux-android \
    && ln -s arm-linux-androideabi-4.9 mipsel-linux-android

# Change timezone
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Asia/Seoul /etc/localtime
