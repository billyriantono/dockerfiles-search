FROM google/cloud-sdk:latest

RUN apt-get update && apt-get install default-jdk -y && apt-get install wget -y && apt-get install unzip -y

ARG MAVEN_VERSION=3.5.4
ARG USER_HOME_DIR="/root"
ARG SHA=ce50b1c91364cb77efe3776f756a6d92b76d9038b0a0782f7d53acf1e997a14d
ARG BASE_URL=https://apache.osuosl.org/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz

RUN mkdir -p /usr/share/maven /usr/share/maven/ref && \
	curl -fsSL -o /tmp/apache-maven.tar.gz ${BASE_URL} && \
	echo "${SHA}  /tmp/apache-maven.tar.gz" | sha256sum -c - && \
	tar -xzf /tmp/apache-maven.tar.gz -C /usr/share/maven --strip-components=1 && \
	rm -f /tmp/apache-maven.tar.gz && \
	ln -s /usr/share/maven/bin/mvn /usr/bin/mvn && \
	wget https://services.gradle.org/distributions/gradle-5.1.1-bin.zip && \
	mkdir /opt/gradle && \
	unzip -d /opt/gradle gradle-5.1.1-bin.zip && \
	export PATH=$PATH:/opt/gradle/gradle-5.1.1/bin && \
	export GRADLE_OPTS=-Xmx1000m
ENV MAVEN_HOME=/usr/share/maven MAVEN_CONFIG="$USER_HOME_DIR/.m2"
CMD mvn -Dapp.devserver.host="0.0.0.0" appengine:run
