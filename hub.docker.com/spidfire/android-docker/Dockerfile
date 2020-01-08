FROM java:8

RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get install -y \
    ruby \
    ruby-dev \
    build-essential \
    libmagickwand-dev \
    lib32stdc++6 \
    lib32z1 \
    zip \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

# Download Android SDK
RUN curl -L "http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz" | tar --no-same-owner -xz -C /opt
ENV ANDROID_HOME /opt/android-sdk-linux
ENV ANDROID_SDK /opt/android-sdk-linux
ENV PATH $ANDROID_HOME/tools:$ANDROID_HOME/platform-tools:$PATH

# Install Android SDK components
RUN echo y | /opt/android-sdk-linux/tools/android update sdk --no-ui --all --filter "build-tools-24.0.0,android-23,addon-google_apis-google-22,extra-android-m2repository,extra-google-m2repository"

# Install ruby prerequisites
RUN gem install rest-client rmagick sentry-raven selenium-webdriver

ENV JAVA_OPTS "-Xms512m -Xmx1024m"
COPY . /opt/almanapp-android
WORKDIR /opt/almanapp-android/
