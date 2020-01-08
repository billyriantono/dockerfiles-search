FROM alvisisme/docker-ubuntu-non-root-with-utils
LABEL maintainer="Alvis Zhao<alvisisme@gmail.com>"
ENTRYPOINT []
CMD ["/bin/bash"]

ENV ANDROID_NDK_VERSION r14b
ENV ANDROID_NDK_HOME /usr/local/android-ndk-${ANDROID_NDK_VERSION}
ENV PATH ${ANDROID_NDK_HOME}:$PATH

RUN sudo apt-get update && sudo DEBIAN_FRONTEND=noninteractive apt-get -y install unzip python make
RUN wget https://dl.google.com/android/repository/android-ndk-${ANDROID_NDK_VERSION}-linux-x86_64.zip && \
   sudo unzip android-ndk-${ANDROID_NDK_VERSION}-linux-x86_64.zip -d /usr/local && \
   rm -rf android-ndk-${ANDROID_NDK_VERSION}-linux-x86_64.zip