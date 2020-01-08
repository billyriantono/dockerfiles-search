FROM jacekmarchwicki/android:java8-r24-4-1

# Install Missing Tools
RUN cd /opt && \
  /opt/tools/android-accept-licenses.sh "android-sdk-linux/tools/android update sdk --all --no-ui --filter build-tools-23.0.1"
