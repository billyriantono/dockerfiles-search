#############################################################################
# Base image is set to Alpine:3.9.4
#############################################################################
FROM alpine:3.9.4

#############################################################################
# Install bash and git commands
#############################################################################
RUN apk update \
	&& apk add \
	openssh-client \
	ca-certificates \
	bash \
	git;

#############################################################################
# Set Java version and URL of Open JDK 13 download
#############################################################################
ENV JAVA_HOME /opt/openjdk-13
ENV PATH $JAVA_HOME/bin:$PATH
ENV JAVA_VERSION 13-ea+19
ENV JAVA_URL https://download.java.net/java/early_access/alpine/19/binaries/openjdk-13-ea+19_linux-x64-musl_bin.tar.gz
ENV JAVA_SHA256 010ea985fba7e3d89a9170545c4e697da983cffc442b84e65dba3baa771299a5

#############################################################################
# Download and extract Open JDK 13 
# https://github.com/docker-library/openjdk/issues/212#issuecomment-420979840
# https://openjdk.java.net/jeps/341
#############################################################################
RUN set -o errexit -o nounset; \
	wget --no-verbose -O /openjdk.tgz "$JAVA_URL"; \
	echo "$JAVA_SHA256 */openjdk.tgz" | sha256sum -c -; \
	mkdir -p "$JAVA_HOME"; \
	tar --extract --file /openjdk.tgz --directory "$JAVA_HOME" --strip-components 1; \
	rm /openjdk.tgz; \
	rm "$JAVA_HOME/lib/src.zip"; \
	java -Xshare:dump;

#############################################################################
# Set Ant version and URL of Ant download
#############################################################################
ENV ANT_HOME /opt/apache-ant-1.10.6
ENV PATH $ANT_HOME/bin:$PATH
ENV ANT_VERSION 1.10.6
ENV ANT_URL https://www-eu.apache.org/dist//ant/binaries/apache-ant-1.10.6-bin.tar.gz

#############################################################################
# Download and extract apache-ant-1.10.6
#############################################################################
RUN set -o errexit -o nounset; \
	wget --no-verbose -O /ant.tgz "$ANT_URL"; \
	mkdir -p "$ANT_HOME"; \
	tar --extract --file /ant.tgz --directory "$ANT_HOME" --strip-components 1; \
	rm /ant.tgz;

#############################################################################
# Set Maven version and URL of Maven download
#############################################################################
ENV M2_HOME /opt/apache-maven-3.6.1
ENV MAVEN_HOME $M2_HOME
ENV PATH $M2_HOME/bin:$PATH
ENV MAVEN_VERSION 3.6.1
ENV M2_VERSION $MAVEN_VERSION
ENV MAVEN_URL https://www-us.apache.org/dist/maven/maven-3/3.6.1/binaries/apache-maven-3.6.1-bin.tar.gz

#############################################################################
# Download and extract apache-maven-3.6.1
#############################################################################
RUN set -o errexit -o nounset; \
	wget --no-verbose -O /maven.tgz "$MAVEN_URL"; \
	mkdir -p "$M2_HOME"; \
	tar --extract --file /maven.tgz --directory "$M2_HOME" --strip-components 1; \
	rm /maven.tgz;

#############################################################################
# Set env for Gradle
#############################################################################
ENV GRADLE_HOME /opt/gradle-5.4.1
ENV PATH $GRADLE_HOME/bin:$PATH
ENV GRADLE_VERSION 5.4.1
ENV GRADLE_URL https://services.gradle.org/distributions/gradle-5.4.1-bin.zip
ARG GRADLE_DOWNLOAD_SHA256=7bdbad1e4f54f13c8a78abc00c26d44dd8709d4aedb704d913fb1bb78ac025dc

#############################################################################
# Download and extract gradle-5.4.1
#############################################################################
RUN set -o errexit -o nounset; \
	echo "Downloading Gradle"; \
	wget --no-verbose -O /gradle.zip https://services.gradle.org/distributions/gradle-5.4.1-bin.zip; \
	echo "Checking download hash"; \
	echo "$GRADLE_DOWNLOAD_SHA256 */gradle.zip" | sha256sum -c -; \
	mkdir -p /opt/gradle; \
	unzip /gradle.zip -d /opt/gradle; \
	rm /gradle.zip; \
	mv /opt/gradle/gradle-5.4.1 /opt; \
	rm -R /opt/gradle;

#############################################################################
# Testing installation
#############################################################################
RUN set -o errexit -o nounset; \
	echo "Testing installation"; \
	java --version; \
	javac --version; \
	ant -version; \
	mvn --version; \
	gradle -v;

#############################################################################
# Set sh prompt
#############################################################################
CMD ["/bin/sh"]
