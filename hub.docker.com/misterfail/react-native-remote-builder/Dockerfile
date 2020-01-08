FROM node

WORKDIR /lib

# Install OpenJDK
RUN apt update && apt install -y \
    openjdk-8-jdk \
    && rm -rf /var/lib/apt/lists/*

# Install Android SDK
RUN wget -q -O sdk.zip https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip && \
    mkdir android-sdk && unzip -qq -d android-sdk sdk.zip && rm -rf sdk.zip && \
    yes | ./android-sdk/tools/bin/sdkmanager "build-tools;27.0.3" "platforms;android-27"

ENV ANDROID_HOME=/lib/android-sdk


# Set project
WORKDIR /root/builder

RUN npm init --yes
RUN npm install --save express formidable path child_process uuid util
RUN npm install -g react-native-cli

RUN mkdir build

COPY src/app.js .
COPY src/build.sh .

RUN chmod +x /root/builder/build.sh

CMD ["node", "app.js"]