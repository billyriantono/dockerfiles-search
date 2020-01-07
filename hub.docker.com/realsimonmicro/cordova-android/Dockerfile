FROM debian:stretch
RUN apt-get update

# Install java
RUN apt-get install -y openjdk-8-jdk-headless
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64

# Install gradle
RUN apt-get install -y gradle

# Install npm
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get install -y nodejs
RUN npm install -g cordova

# Install android SDK
RUN apt-get install -y wget zip
WORKDIR /opt
RUN wget https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip
RUN unzip sdk-tools-linux-4333796.zip -d android
WORKDIR /opt/android/tools/bin
RUN yes | ./sdkmanager --update
ENV PATH=$PATH:/opt/android/tools/bins
ENV ANDROID_HOME=/opt/android

# Install the android SDK build tools
RUN yes | ./sdkmanager --install "build-tools;29.0.2"

# Setup example workspace
WORKDIR /workspace-example
RUN cordova telemetry off
RUN cordova create ./ com.example.hello HelloWorld
RUN cordova platform add android
RUN cordova platform add browser
# Now you can run `cordova build` with `--debug` or `--release` to create the example android app

# Setup workspace
WORKDIR /workspace
