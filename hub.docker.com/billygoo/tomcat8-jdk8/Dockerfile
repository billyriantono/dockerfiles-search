FROM tomcat:8.0-jre8

# install openjdk-8
RUN set -x \
        && apt-get update \
        && apt-get install -y \
           openjdk-8-jdk \
        && rm -rf /var/lib/apt/lists/*
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
