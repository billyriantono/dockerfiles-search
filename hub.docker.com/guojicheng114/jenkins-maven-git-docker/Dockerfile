# Pre-Built Docker Jenkins Images
# Maven 3 installed
# Bundled with Maven3 pre-installed
# Jenkins Git plugin installed
# Jenkins CloudBees Docker Build and Publish plugin installed
# Build Pipeline Plugin installed
# 
# As used on blog describing continuous delivery Jenkins, Docker and Spring Boot
# http://eggsylife.co.uk/2015/12/29/spring-boot-jenkins-and-docker-part-one/

FROM jenkins/jenkins:lts
MAINTAINER James Heggs jimbobegg@hotmail.com

# Install Jenkins Plugins
COPY resources/plugins.txt /usr/share/jenkins/plugins.txt
RUN /usr/local/bin/install-plugins.sh </usr/share/jenkins/plugins.txt

# Configure Maven installation location in Jenkins
COPY resources/hudson.tasks.Maven.xml /var/jenkins_home/hudson.tasks.Maven.xml

# Copy Docker config
COPY resources/org.jenkinsci.plugins.docker.commons.tools.DockerTool.xml /var/jenkins_home/org.jenkinsci.plugins.docker.commons.tools.DockerTool.xml

# Install maven
USER root
RUN apt-get update && apt-get install -y wget

# get maven 3.2.2
RUN wget --no-verbose -O /tmp/apache-maven-3.2.2.tar.gz http://archive.apache.org/dist/maven/maven-3/3.2.2/binaries/apache-maven-3.2.2-bin.tar.gz

# verify checksum
RUN echo "87e5cc81bc4ab9b83986b3e77e6b3095 /tmp/apache-maven-3.2.2.tar.gz" | md5sum -c

# install maven
RUN tar xzf /tmp/apache-maven-3.2.2.tar.gz -C /opt/
RUN ln -s /opt/apache-maven-3.2.2 /opt/maven
RUN ln -s /opt/maven/bin/mvn /usr/local/bin
RUN rm -f /tmp/apache-maven-3.2.2.tar.gz
ENV MAVEN_HOME /opt/maven

# install depdency
RUN apt-get install -y unzip openssl ca-certificates libltdl7 
# install gradle 
ENV GRADLE_HOME /opt/gradle
ENV GRADLE_VERSION 4.6
ARG GRADLE_DOWNLOAD_SHA256=98bd5fd2b30e070517e03c51cbb32beee3e2ee1a84003a5a5d748996d4b1b915
RUN wget -O gradle.zip "https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip" \
        && echo "Checking download hash" \
        && echo "${GRADLE_DOWNLOAD_SHA256} *gradle.zip" | sha256sum -c - \
\
	&& echo "Installing Gradle" \
	&& unzip gradle.zip \
	&& rm gradle.zip \
	&& mv "gradle-${GRADLE_VERSION}" "${GRADLE_HOME}/" \
	&& ln --symbolic "${GRADLE_HOME}/bin/gradle" /usr/bin/gradle
 
