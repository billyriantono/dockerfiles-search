FROM openjdk:8-jdk-alpine

#Configure version variables
ENV MAVEN_VERSION=3.5.0 \
    MAVEN_USER_HOME_DIR="/root"

#Configure paths
ENV MAVEN_BASE_URL=https://apache.osuosl.org/maven/maven-3/${MAVEN_VERSION}/binaries \
    MAVEN_SHA=beb91419245395bd69a4a6edad5ca3ec1a8b64e41457672dc687c173a495f034 \
    MAVEN_HOME=/usr/share/maven \
    MAVEN_CONFIG="${MAVEN_USER_HOME_DIR}/.m2"

#Install Curl
RUN apk --no-cache add curl

#Install Maven
RUN mkdir -p /usr/share/maven /usr/share/maven/ref \
  && curl -fsSL -o /tmp/apache-maven.tar.gz ${MAVEN_BASE_URL}/apache-maven-${MAVEN_VERSION}-bin.tar.gz \
  && echo "${MAVEN_SHA}  /tmp/apache-maven.tar.gz" | sha256sum -c - \
  && tar -xzf /tmp/apache-maven.tar.gz -C /usr/share/maven --strip-components=1 \
  && rm -f /tmp/apache-maven.tar.gz \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn
