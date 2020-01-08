FROM circleci/android:api-28-node

ENV CORDOVA_VERSION=9.0.0
ENV GRADLE_VERSION=5.6.4

RUN sudo npm -g i cordova@${CORDOVA_VERSION}

RUN wget --no-verbose --output-document=/tmp/gradle.zip "https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip" \
    && sudo unzip -d /opt /tmp/gradle.zip \
    && sudo mv /opt/gradle-${GRADLE_VERSION} /opt/gradle \
    && sudo ln -s /opt/gradle/bin/gradle /usr/local/bin/gradle \
    && rm /tmp/gradle.zip