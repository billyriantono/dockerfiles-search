FROM circleci/android:api-29-node

RUN sudo apt-get update && sudo apt-get install -y gradle rsync
RUN (cd / && sudo npm install -g cordova@latest)
RUN (cd / && sudo npm install -g ionic@latest)
RUN (cd / && sudo npm install -g cordova-res@latest --unsafe-perm=true --allow-root)

RUN yes | sdkmanager --update

ENV ANDROID_SDK_ROOT $ANDROID_HOME
ENV PATH $PATH:$ANDROID_SDK_ROOT/build-tools/29.0.2
