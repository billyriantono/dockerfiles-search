FROM openjdk:11.0.1-jdk-sid

ENV MAVEN_VERSION=3.3.9
ENV MAVEN_HOME=/opt/mvn

# change to tmp folder
WORKDIR /tmp

RUN apt-get update && apt-get install -y --no-install-recommends \
		wget \
        tar \
	&& rm -rf /var/lib/apt/lists/*

# Download and extract maven to opt folder
RUN wget --no-check-certificate --no-cookies http://archive.apache.org/dist/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz \
    && wget --no-check-certificate --no-cookies http://archive.apache.org/dist/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz.md5 \
    && echo "$(cat apache-maven-${MAVEN_VERSION}-bin.tar.gz.md5) apache-maven-${MAVEN_VERSION}-bin.tar.gz" | md5sum -c \
    && tar -zvxf apache-maven-${MAVEN_VERSION}-bin.tar.gz -C /opt/ \
    && ln -s /opt/apache-maven-${MAVEN_VERSION} /opt/mvn \
    && rm -f apache-maven-${MAVEN_VERSION}-bin.tar.gz \
    && rm -f apache-maven-${MAVEN_VERSION}-bin.tar.gz.md5

#RUN wget --no-check-certificate --no-cookies http://download2.gluonhq.com/openjfx/11/openjfx-11_linux-x64_bin-sdk.zip 
#    && unzip openjfx-11_linux-x64_bin-sdk.zip -d /opt/ \


# add executables to path
RUN update-alternatives --install "/usr/bin/mvn" "mvn" "/opt/mvn/bin/mvn" 1 && \
    update-alternatives --set "mvn" "/opt/mvn/bin/mvn"

# basic tests
RUN mvn --version

# change to root folder
WORKDIR /root
