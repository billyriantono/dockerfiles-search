# This is based on the Dockerfile from https://index.docker.io/u/wasabeef/android/
# base for this file was https://github.com/camlistore/camlistore/blob/master/clients/android/devenv/Dockerfile

FROM centos
MAINTAINER Felix Mann <djflix@gmail.com>

# Epel
# RUN rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm

# Install Development Tools
RUN yum -y groupinstall "Development Tools"

# yum update
RUN yum -y update

# Install java (OpenJDK) and 32bit Library
RUN yum -y install java-1.8.0-openjdk-devel glibc.i686 libstdc++.i686 glibc-devel.i686 zlib-devel.i686 ncurses-devel.i686 libX11-devel.i686 libXrender.i686 && yum clean all

# Install Android SDK

RUN mkdir /usr/local/android-sdk-linux && cd /usr/local/android-sdk-linux && curl -L -O https://dl.google.com/android/repository/tools_r25.2.3-linux.zip && unzip -o tools_r25.2.3-linux.zip && rm -rf /usr/local/android-sdk-linux/android-sdk_r25.2.3-linux.tgz

# Preactivate Android SDK
RUN mkdir -p /usr/local/android-sdk-linux/licenses && echo -n -e "\n8933bad161af4178b1185d1a37fbf41ea5269c55" > /usr/local/android-sdk-linux/licenses/android-sdk-license

# Install Android tools
RUN echo y | /usr/local/android-sdk-linux/tools/android update sdk --filter tools --no-ui --force -a
RUN echo y | /usr/local/android-sdk-linux/tools/android update sdk --filter platform-tools --no-ui --force -a
RUN echo y | /usr/local/android-sdk-linux/tools/android update sdk --filter android-24 --no-ui --force -a

# Install Apache-Ant
RUN cd /usr/local/ && curl -L -O http://www-us.apache.org/dist//ant/binaries/apache-ant-1.10.1-bin.tar.gz && tar xf apache-ant-1.10.1-bin.tar.gz && rm -rf apache-ant-1.10.1-bin.tar.gz

# Install Maven
# RUN cd /usr/local/ && curl -L -O http://www-us.apache.org/dist/maven/maven-3/3.5.0/binaries/apache-maven-3.5.0-bin.tar.gz && tar xf apache-maven-3.5.0-bin.tar.gz && rm -rf apache-maven-3.5.0-bin.tar.gz

# Install Gradle
RUN cd /usr/local/ && curl -L -O http://services.gradle.org/distributions/gradle-3.5-bin.zip && unzip -o gradle-3.5-bin.zip && rm -rf gradle-3.5-bin.zip

# Environment variables
ENV JAVA_HOME /usr/lib/jvm/jre-1.8.0-openjdk
ENV PATH $JAVA_HOME/bin:$PATH

ENV ANDROID_HOME /usr/local/android-sdk-linux
ENV ANT_HOME /usr/local/apache-ant-1.10.1
# ENV MAVEN_HOME /usr/local/apache-maven-3.5.0
ENV GRADLE_HOME /usr/local/gradle-3.5
ENV PATH $PATH:$ANDROID_HOME/tools
ENV PATH $PATH:$ANDROID_HOME/platform-tools
ENV PATH $PATH:$ANT_HOME/bin
ENV PATH $PATH:$MAVEN_HOME/bin
ENV PATH $PATH:$GRADLE_HOME/bin

# Clean up
RUN yum clean all

ENV ANDROID_HOME /usr/local/android-sdk-linux
ENV ANT_HOME /usr/local/apache-ant-1.10.1
ENV PATH $PATH:$ANDROID_HOME/tools
ENV PATH $PATH:$ANDROID_HOME/platform-tools
ENV PATH $PATH:$ANT_HOME/bin
ENV IN_DOCKER 1
