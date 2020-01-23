FROM openjdk:11.0.3-jdk-stretch

### Gradle
WORKDIR /usr/local/chrome

ENV GRADLE_HOME /opt/gradle
ENV GRADLE_VERSION 6.0.1

ARG GRADLE_DOWNLOAD_SHA256=d364b7098b9f2e58579a3603dc0a12a1991353ac58ed339316e6762b21efba44

RUN set -o errexit -o nounset \
    && echo "Downloading Gradle" \
    && wget --no-verbose --output-document=gradle.zip "https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip" \
    \
    && echo "Checking download hash" \
    && echo "${GRADLE_DOWNLOAD_SHA256} *gradle.zip" | sha256sum --check - \
    \
    && echo "Installing Gradle" \
    && unzip gradle.zip \
    && rm gradle.zip \
    && mv "gradle-${GRADLE_VERSION}" "${GRADLE_HOME}/" \
    && ln --symbolic "${GRADLE_HOME}/bin/gradle" /usr/bin/gradle \
    \
    && echo "Testing Gradle installation" \
    && gradle --version

### Chrome
WORKDIR /usr/local/chrome

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list

RUN apt update && apt install -y google-chrome-stable \
    unzip \
    apt-transport-https

### Google Cloud SDK
WORKDIR /usr/local/cloud-sdk

RUN export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" \
    && echo "deb https://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" > /etc/apt/sources.list.d/google-cloud-sdk.list \
    && curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -

RUN apt update && apt install -y google-cloud-sdk \
    kubectl

### Yarn
WORKDIR /usr/local/yarn

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt update && apt install -y --no-install-recommends yarn

### Angular
ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 12.13.0

WORKDIR $NVM_DIR

RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.0/install.sh | bash \
    && sh $NVM_DIR/nvm.sh \
    && [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" \
    && nvm install $NODE_VERSION \
    && npm config set user 0 && npm config set unsafe-perm true \
    && npm install -g @angular/cli \
    && rm install.sh

ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

WORKDIR /
