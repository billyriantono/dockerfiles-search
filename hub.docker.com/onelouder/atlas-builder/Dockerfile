FROM alpine:3.9

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

ENV NODE_VERSION=10.14.2-r0

RUN apk -U --no-cache add \
  nodejs-npm="${NODE_VERSION}" \
  docker \
  git

# add a simple script that can auto-detect the appropriate JAVA_HOME value
# based on whether the JDK or only the JRE is installed
RUN { \
		echo '#!/bin/sh'; \
		echo 'set -e'; \
		echo; \
		echo 'dirname "$(dirname "$(readlink -f "$(which javac || which java)")")"'; \
	} > /usr/local/bin/docker-java-home \
	&& chmod +x /usr/local/bin/docker-java-home
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV PATH $PATH:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin

ENV JAVA_VERSION 8u222
ENV JAVA_ALPINE_VERSION 8.222.10-r0

RUN set -x \
	&& apk add --no-cache \
		openjdk8="$JAVA_ALPINE_VERSION" \
	&& [ "$JAVA_HOME" = "$(docker-java-home)" ]

ARG GRADLE_DOWNLOAD_SHA256=af334d994b5e69e439ab55b5d2b7d086da5ea6763d78054f49f147b06370ed71
ARG MAVEN_VERSION=3.6.2
ARG MAVEN_DOWNLOAD_SHA256=3fbc92d1961482d6fbd57fbf3dd6d27a4de70778528ee3fb44aa7d27eb32dfdc
ARG BASE_URL=https://apache.osuosl.org/maven/maven-3/${MAVEN_VERSION}/binaries

ENV GRADLE_HOME /opt/gradle
ENV GRADLE_VERSION 4.8.1
ENV MAVEN_HOME /opt/maven
ENV MAVEN_CONFIG /home/build/.m2

RUN set -o errexit -o nounset \
	&& echo "Installing build dependencies" \
	&& apk add --no-cache --virtual .build-deps \
		openssl \
		unzip \
    tar \
	\
	&& echo "Downloading Gradle" \
	&& wget -O gradle.zip "https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip" \
	\
	&& echo "Checking download hash" \
	&& echo "${GRADLE_DOWNLOAD_SHA256} *gradle.zip" | sha256sum -c - \
	\
	&& echo "Installing Gradle" \
	&& unzip gradle.zip \
	&& rm gradle.zip \
	&& mkdir -p /opt \
	&& mv "gradle-${GRADLE_VERSION}" "${GRADLE_HOME}/" \
	&& ln -s "${GRADLE_HOME}/bin/gradle" /usr/bin/gradle \
	\
	&& apk del .build-deps \
	\
	&& echo "Adding build user and group" \
	&& addgroup -S -g 1000 build \
	&& adduser -D -S -G build -u 1000 -s /bin/ash build \
	&& mkdir /home/build/.gradle \
	&& chown -R build:build /home/build \
	\
	&& echo "Symlinking root Gradle cache to build Gradle cache" \
	&& ln -s /home/build/.gradle /root/.gradle \
  \
  && echo "Downloading and installing Maven" \
  && mkdir -p /opt/maven /opt/maven/ref \
  && wget -O maven.tar.gz "${BASE_URL}/apache-maven-${MAVEN_VERSION}-bin.tar.gz" \
  && echo "${MAVEN_DOWNLOAD_SHA256} *maven.tar.gz" | sha256sum -c - \
  && tar -xzf maven.tar.gz -C /opt/maven --strip-components=1 \
  && rm maven.tar.gz \
  \
  && echo "Symlinking root Maven cache to build Maven cache" \
  && ln -s /opt/maven/bin/mvn /usr/bin/mvn \
  && ln -s /home/build/.m2 root/.m2

# Create build volume
USER build
VOLUME ["/home/build/.gradle", "/home/build/.m2"]
WORKDIR /home/build
  
COPY settings-docker.xml /usr/share/maven/ref/
