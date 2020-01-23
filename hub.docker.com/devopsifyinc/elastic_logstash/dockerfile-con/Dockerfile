FROM  mingc/android-build-box:latest

MAINTAINER Mariano Heredia

RUN echo "installing latest sdk tools" && \
     yes | "$ANDROID_HOME"/tools/bin/sdkmanager \
          "platforms;android-28" && \
     yes | "$ANDROID_HOME"/tools/bin/sdkmanager \
          "build-tools;28.0.3"

RUN echo "installing bundler" && gem install bundler
