FROM runmymind/docker-android-sdk:ubuntu-standalone

ENV NODE_VERSION=12.13.0 \
    NPM_CONFIG_PREFIX=/home/node/.npm-global \
    PATH=${PATH}:${ANDROID_HOME}/emulator:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools:/opt/node/bin:/home/node/.npm-global/bin

RUN echo "=== Remove NodeJS from original image  ===" \
    && apt remove nodejs -y \
    && echo "=== I386 architecture for installing libraries for NodeJS ===" \
    && dpkg --add-architecture i386 \
    && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
    yarn \
    libc6:i386 \
    libncurses5:i386 \
    libstdc++6:i386 \
    lib32z1 \
    g++ \
    python3.7 \
    && echo "=== NodeJS ===" \
    && mkdir -p /home/node/.npm-global \
    && wget -q http://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.gz \
    && tar -xzf node-v${NODE_VERSION}-linux-x64.tar.gz \
    && mv node-v${NODE_VERSION}-linux-x64 /opt/node \
    && rm node-v${NODE_VERSION}-linux-x64.tar.gz \
    && echo "=== React Native CLI ===" \
    && npm install -g react-native-cli \
    && npm install -g npm \
    && echo "=== Cleaning of unused packages ===" \
    && apt-get autoremove -y \
    && apt-get clean

WORKDIR /project