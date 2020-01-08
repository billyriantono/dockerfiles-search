FROM jenkins:latest
MAINTAINER eq2k "eq2k@hotmail.com"

USER root

# Android and other dependencies
RUN apt-get update && apt-get install -y --no-install-recommends git expect lib32stdc++6 lib32z1 && apt-get install -y build-essential

# Clean up
RUN apt-get clean

# Download and extract Android SDK
#RUN cd /opt && wget --output-document=android-sdk.tgz --quiet http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz 
#RUN cd /opt && tar xzf android-sdk.tgz 
#RUN cd /opt && rm -f android-sdk.tgz 
#RUN cd /opt && chmod -R +xr android-sdk-linux
#RUN cd /opt/android-sdk-linux/tools && android update sdk --no-ui

# Download and extract Android NDK
#RUN cd /opt && wget --output-document=android-ndk-r10e.bin --quiet http://dl.google.com/android/ndk/android-ndk-r10e-linux-x86_64.bin
#RUN cd /opt && chmod a+x android-ndk-r10e.bin
#RUN cd /opt && ./android-ndk-r10e.bin
#RUN cd /opt && rm -f android-ndk-r10e.bin
#RUN cd /opt && mv android-ndk-r10e android-ndk-linux
#RUN cd /opt && chmod -R +xr android-ndk-linux

# Android SDK/NDK paths
ENV ANDROID_HOME /var/jenkins_home/android-sdk-linux
ENV ANDROID_NDK_HOME /var/jenkins_home/android-ndk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools:${ANDROID_NDK_HOME}

# Copy Android SDK/NDK to volume on entry

#USER jenkins
#COPY android-install.sh /usr/local/bin/android-install.sh
#ENTRYPOINT ["/bin/tini", "--", "/usr/local/bin/jenkins.sh", "/usr/local/bin/android-install.sh"]