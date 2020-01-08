# CentOS based
FROM centos:7
MAINTAINER Miroslav Svoboda <miroslav.svoboda@karumien.com>

# Set environment variables for versions
ENV JAVA_VERSION=8 \
    JAVA_UPDATE=152 \
    JAVA_BUILD=16 \
    JAVA_PATH=aa0333dd3019491ca4f6ddbe78cdb6d0 \
    JAVA_HOME="/opt/java"
    
ENV PATH $PATH:$JAVA_HOME/bin

# Install utils
RUN yum update -y && \ 
    yum install -y wget && \
    yum install -y unzip && \
    yum install -y git && \
    yum clean all
    
# Change to tmp folder
WORKDIR /tmp

# Download and extract jdk to opt folder
RUN wget --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie;" \
        "http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}u${JAVA_UPDATE}-b${JAVA_BUILD}/${JAVA_PATH}/jdk-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.rpm" && \
    yum localinstall -y jdk-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.rpm  && \
    ln -s "/usr/java/jdk1.${JAVA_VERSION}.0_${JAVA_UPDATE}" "$JAVA_HOME" && \
    wget --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie;" \
        "http://download.oracle.com/otn-pub/java/jce/${JAVA_VERSION}/jce_policy-${JAVA_VERSION}.zip" && \
    unzip -jo -d "${JAVA_HOME}/jre/lib/security" "jce_policy-${JAVA_VERSION}.zip" && \
    rm -rf "jce_policy-${JAVA_VERSION}.zip"
    
# Optimize JDK8 size 
RUN rm -rf $JAVA_HOME/*src.zip \
           $JAVA_HOME/lib/missioncontrol \
           $JAVA_HOME/lib/visualvm \
           $JAVA_HOME/lib/*javafx* \
           $JAVA_HOME/jre/lib/security/README.txt \
           $JAVA_HOME/jre/lib/plugin.jar \
           $JAVA_HOME/jre/lib/ext/jfxrt.jar \
           $JAVA_HOME/jre/bin/javaws \
           $JAVA_HOME/jre/lib/javaws.jar \
           $JAVA_HOME/jre/lib/desktop \
           $JAVA_HOME/jre/plugin \
           $JAVA_HOME/jre/lib/deploy* \
           $JAVA_HOME/jre/lib/*javafx* \
           $JAVA_HOME/jre/lib/*jfx* \
           $JAVA_HOME/jre/lib/amd64/libdecora_sse.so \
           $JAVA_HOME/jre/lib/amd64/libprism_*.so \
           $JAVA_HOME/jre/lib/amd64/libfxplugins.so \
           $JAVA_HOME/jre/lib/amd64/libglass.so \
           $JAVA_HOME/jre/lib/amd64/libgstreamer-lite.so \
           $JAVA_HOME/jre/lib/amd64/libjavafx*.so \
           $JAVA_HOME/jre/lib/amd64/libjfx*.so
    
# Add executables to path
RUN update-alternatives --install "/usr/bin/java" "java" "/opt/java/bin/java" 1 && \
    update-alternatives --set "java" "/opt/java/bin/java" && \
    update-alternatives --install "/usr/bin/javac" "javac" "/opt/java/bin/javac" 1 && \
    update-alternatives --set "javac" "/opt/java/bin/javac" && \
    update-alternatives --install "/usr/bin/keytool" "keytool" "/opt/java/bin/keytool" 1 && \
    update-alternatives --set "keytool" "/opt/java/bin/keytool"

# Force Docker to use UTF-8 encodings
ENV LANG C.UTF-8

# Maven install
ENV MAVEN_VERSION=3.5.2
ENV MAVEN_HOME=/opt/mvn
ENV PATH $PATH:$MAVEN_HOME/bin

# Download and extract maven to opt folder
RUN wget --no-check-certificate --no-cookies https://repo1.maven.org/maven2/org/apache/maven/apache-maven/${MAVEN_VERSION}/apache-maven-${MAVEN_VERSION}-bin.tar.gz && \
    wget --no-check-certificate --no-cookies https://repo1.maven.org/maven2/org/apache/maven/apache-maven/${MAVEN_VERSION}/apache-maven-${MAVEN_VERSION}-bin.tar.gz.md5 && \
    echo "$(cat apache-maven-${MAVEN_VERSION}-bin.tar.gz.md5) apache-maven-${MAVEN_VERSION}-bin.tar.gz" | md5sum -c && \
    tar -zvxf apache-maven-${MAVEN_VERSION}-bin.tar.gz -C /opt/ && \
    ln -s /opt/apache-maven-${MAVEN_VERSION} /opt/mvn && \
    rm -f apache-maven-${MAVEN_VERSION}-bin.tar.gz && \
    rm -f apache-maven-${MAVEN_VERSION}-bin.tar.gz.md5

# Add executables to path
RUN update-alternatives --install "/usr/bin/mvn" "mvn" "/opt/mvn/bin/mvn" 1 && \
    update-alternatives --set "mvn" "/opt/mvn/bin/mvn" 

# Cleaning
RUN rm -rf /tmp/* && \
    rm -rf /var/cache/yum

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

# Define default command.
CMD ["bash"]
