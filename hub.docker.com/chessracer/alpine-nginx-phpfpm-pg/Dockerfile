FROM java:8
LABEL author chensy<chensy@primeton.com>

ARG GRADLE_VERSION=3.0
ARG GRADLE_URL=https://downloads.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip
ARG GRADLE_SHA256=39c906941a474444afbddc38144ed44166825acb0a57b0551dddb04bbf157f80

ENV GRADLE_HOME /opt/gradle-${GRADLE_VERSION}
ENV PATH $PATH:${GRADLE_HOME}/bin

RUN wget -O gradle.zip ${GRADLE_URL} \
    && echo "$GRADLE_SHA256 gradle.zip" | sha256sum -c - \
    && unzip gradle.zip -d /opt \
    && rm -rf gradle.zip 

USER root

WORKDIR ${GRADLE_HOME}

ENTRYPOINT ["gradle"]
