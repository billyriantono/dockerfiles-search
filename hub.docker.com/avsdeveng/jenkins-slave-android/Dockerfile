FROM ubuntu:xenial

# Java Env Variables
ENV JAVA_VERSION=1.8.0_144
ENV JAVA_TARBALL=server-jre-8u144-linux-x64.tar.gz
ENV JAVA_HOME=/opt/java/jdk${JAVA_VERSION}
ENV JAVA_MAGIC="090f390dda5b47b9b721c7dfaa008135"
ENV JAVA_VERSION_BUILD="8u144-b01"

# Android
ENV ANDROID_HOME=/opt/android-sdk-linux
ENV ANDROID_TOOLS_VER="r25.2.5"
ENV ANDROID_NDK_VER="r15c"

# Maven, Ant, Gradle
ENV MAVEN_VER="3.5.0"
ENV ANT_VER="1.10.1"
ENV GRADLE_VER="4.0.1"

# Swarm Env Variables (defaults)
ENV SWARM_MASTER=http://jenkins:8080/jenkins/
ENV SWARM_USER=jenkins
ENV SWARM_PASSWORD=jenkins

# Slave Env Variables
ENV SLAVE_NAME="Swarm_Slave"
ENV SLAVE_LABELS="docker androidsdk"
ENV SLAVE_MODE="exclusive"
ENV SLAVE_EXECUTORS=4
ENV SLAVE_DESCRIPTION="Core Jenkins Slave"
ENV SWARM_CLIENT_VERSION="2.2"

# Make Ubuntu clean again
RUN echo 'DPkg::Post-Invoke { "rm -f /var/cache/apt/archives/*.deb /var/cache/apt/archives/partial/*.deb /var/cache/apt/*.bin || true"; };' > /etc/apt/apt.conf.d/docker-clean
RUN echo 'APT::Update::Post-Invoke { "rm -f /var/cache/apt/archives/*.deb /var/cache/apt/archives/partial/*.deb /var/cache/apt/*.bin || true"; };' >> /etc/apt/apt.conf.d/docker-clean
RUN echo 'Dir::Cache::pkgcache ""; Dir::Cache::srcpkgcache "";' >> /etc/apt/apt.conf.d/docker-clean

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y upgrade && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y curl wget unzip bzip2

# Install Java
RUN wget -q --no-check-certificate --directory-prefix=/tmp --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" \
            http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_BUILD}/${JAVA_MAGIC}/${JAVA_TARBALL}
RUN mkdir -p /opt/java && tar -xzf /tmp/${JAVA_TARBALL} -C /opt/java/
RUN update-alternatives --install "/usr/bin/java" "java" "/opt/java/jdk${JAVA_VERSION}/bin/java" 100 && \
    update-alternatives --install "/usr/bin/javac" "javac" "/opt/java/jdk${JAVA_VERSION}/bin/javac" 100 && \
    update-alternatives --set java /opt/java/jdk${JAVA_VERSION}/bin/java && \
    update-alternatives --set javac /opt/java/jdk${JAVA_VERSION}/bin/javac

# Android dependencies
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y libc6-i386 lib32stdc++6 lib32gcc1 lib32ncurses5 lib32z1 && \
    apt-get autoremove && apt-get clean
RUN mkdir -p ${ANDROID_HOME} && \
    wget -q --no-check-certificate --directory-prefix=/tmp https://dl.google.com/android/repository/tools_${ANDROID_TOOLS_VER}-linux.zip && \
    unzip -q /tmp/tools_${ANDROID_TOOLS_VER}-linux.zip -d ${ANDROID_HOME} && \
    rm -f /tmp/tools_${ANDROID_TOOLS_VER}-linux.zip && \
    wget -q --no-check-certificate --directory-prefix=/tmp https://dl.google.com/android/repository/android-ndk-${ANDROID_NDK_VER}-linux-x86_64.zip && \
    unzip -q /tmp/android-ndk-${ANDROID_NDK_VER}-linux-x86_64.zip -d ${ANDROID_HOME} && \
    rm -f /tmp/android-ndk-${ANDROID_NDK_VER}-linux-x86_64.zip && \
    mv ${ANDROID_HOME}/android-ndk-${ANDROID_NDK_VER} ${ANDROID_HOME}/ndk-bundle

# Maven, Gradle, Ant
RUN wget -q --no-check-certificate --directory-prefix=/tmp https://www.apache.org/dist/ant/binaries/apache-ant-${ANT_VER}-bin.tar.bz2 && \
    tar jxf /tmp/apache-ant-${ANT_VER}-bin.tar.bz2 -C /opt

RUN wget -q --no-check-certificate --directory-prefix=/tmp https://services.gradle.org/distributions/gradle-${GRADLE_VER}-bin.zip && \
    unzip -q /tmp/gradle-${GRADLE_VER}-bin.zip -d /opt

RUN wget -q --no-check-certificate --directory-prefix=/tmp https://www-us.apache.org/dist/maven/maven-3/${MAVEN_VER}/binaries/apache-maven-${MAVEN_VER}-bin.zip && \
    unzip -q /tmp/apache-maven-${MAVEN_VER}-bin.zip -d /opt

ENV ANT_HOME="/opt/apache-ant-${ANT_VER}"
ENV M2_HOME="/opt/apache-maven-${MAVEN_VER}"
ENV GRADLE_HOME="/opt/gradle-${GRADLE_VER}"

# Tools path
ENV PATH ${ANT_HOME}/bin:${M2_HOME}/bin:${GRADLE_HOME}/bin:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/tools/bin:${PATH}

# SDK and build-tools (desc order)
RUN echo y | android update sdk --no-ui --all --filter platform-tools | grep 'package installed'

RUN echo y | android update sdk --no-ui --all --filter android-25 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter android-24 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter android-23 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter android-22 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter android-21 | grep 'package installed'

RUN echo y | android update sdk --no-ui --all --filter build-tools-25.0.3 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter build-tools-25.0.2 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter build-tools-25.0.1 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter build-tools-25.0.0 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter build-tools-24.0.3 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter build-tools-24.0.2 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter build-tools-24.0.1 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter build-tools-24.0.0 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter build-tools-23.0.3 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter build-tools-23.0.2 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter build-tools-23.0.1 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter build-tools-22.0.1 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter build-tools-21.1.2 | grep 'package installed'

RUN echo y | android update sdk --no-ui --all --filter sys-img-armeabi-v7a-android-24 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter sys-img-armeabi-v7a-android-21 | grep 'package installed'

RUN echo y | android update sdk --no-ui --all --filter extra-android-m2repository | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter extra-google-m2repository | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter extra-google-google_play_services | grep 'package installed'

RUN echo y | android update sdk --no-ui --all --filter addon-google_apis-google-23 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter addon-google_apis-google-22 | grep 'package installed'
RUN echo y | android update sdk --no-ui --all --filter addon-google_apis-google-21 | grep 'package installed'

RUN echo y | sdkmanager --update | grep done

# Logs cleanup
RUN rm -rf /tmp/* && rm -rf /var/log/*

# Make Jenkins a slave by installing swarm-client
RUN curl -s -o /bin/swarm-client.jar -k http://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/${SWARM_CLIENT_VERSION}/swarm-client-${SWARM_CLIENT_VERSION}-jar-with-dependencies.jar

# Start Swarm-Client
CMD java -jar /bin/swarm-client.jar -executors ${SLAVE_EXECUTORS} -description "${SLAVE_DESCRIPTION}" -master ${SWARM_MASTER} -username ${SWARM_USER} -password ${SWARM_PASSWORD} -name "${SLAVE_NAME}" -labels "${SLAVE_LABELS}" -mode ${SLAVE_MODE}
