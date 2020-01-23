FROM java:7-jdk

# Gradle
ENV GRADLE_VERSION 3.1
RUN set -e \
	&& curl -L "https://downloads.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip" -o "/tmp/gradle-${GRADLE_VERSION}-bin.zip" \
	&& unzip -q "/tmp/gradle-${GRADLE_VERSION}-bin.zip" -d /usr/local \
	&& mv "/usr/local/gradle-${GRADLE_VERSION}" /usr/local/gradle \
	&& ln -s /usr/local/gradle/bin/gradle /usr/local/bin/gradle

CMD gradle
