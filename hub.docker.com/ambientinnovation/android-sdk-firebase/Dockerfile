# Author: Patrick Hejnol

# We first get our Baseimage
FROM runmymind/docker-android-sdk:alpine-standalone

# We then set our enviroment-paths as needed
ENV PATH $PATH:$ANDROID_SDK_HOME/platform-tools
ENV PATH $PATH:$ANDROID_SDK_ROOT/platform-tools:$ANDROID_SDK_ROOT/tools/emulator:$ANDROID_SDK_ROOT/tools
ENV PATH $PATH:$ANDROID_SDK_HOME/tools/bin

# After that we update the index of available packages and install python (needed for "gcloud")
RUN apk update
RUN apk add python

# Here we download and install all needed platform-tools, sdks, repositories, etc
# If changing/adding/deleting device configurations, this should be adopted to speed up build times
# Run "sdkmanager --list" for the exact strings
RUN sdkmanager "platform-tools" "platforms;android-28" "platforms;android-28"
RUN sdkmanager "build-tools;28.0.3" "build-tools;28.0.2"
RUN sdkmanager "extras;android;m2repository"
RUN sdkmanager "extras;m2repository;com;android;support;constraint;constraint-layout;1.0.2"
RUN sdkmanager "extras;m2repository;com;android;support;constraint;constraint-layout-solver;1.0.2"
RUN sdkmanager "extras;google;m2repository"
RUN sdkmanager --licenses

# Here we download the "google-cloud-sdk" and move it to "/opt/google-cloud-sdk" (Must be the same as defined in "gitlab-ci.yml")
RUN wget -qO- https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-185.0.0-linux-x86_64.tar.gz | tar xz
RUN mv ./google-cloud-sdk /opt/

# We do this so that we don't have to write out the path to the executable
ENV PATH $PATH:/opt/google-cloud-sdk/bin/

# We update the "google-cloud" components
RUN gcloud components update

# Generate a debug keystore to avoid it being generated on each `docker run`
RUN mkdir ~/.android
RUN keytool -genkeypair -alias androiddebugkey -keypass android -keystore ~/.android/debug.keystore -storepass android -dname "CN=Android Debug,O=Android,C=US" -keyalg RSA -validity 365

