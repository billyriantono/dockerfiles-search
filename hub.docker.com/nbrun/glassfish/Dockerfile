# Based on oracle/glassfish:4.1.2
# See : https://github.com/oracle/docker-images/blob/master/GlassFish/4.1.2/Dockerfile
#
# DO NOT ALTER OR REMOVE COPYRIGHT NOTICES OR THIS HEADER.
# 
# Copyright (c) 2017 Oracle and/or its affiliates. All rights reserved.
# 
# GlassFish on Docker with Oracle Linux and OpenJDK
FROM oraclelinux:7-slim

# Set environment variables and default password for user 'admin'
ENV GLASSFISH_PKG=glassfish-4.1.2.zip \
    GLASSFISH_URL=http://download.oracle.com/glassfish/4.1.2/release/glassfish-4.1.2.zip \
    GLASSFISH_HOME=/glassfish4 \
    MD5=9a37928ea6e54334101b8a89e03a8d7d \
    PATH=$PATH:/glassfish4/bin \
    JAVA_HOME=/usr/lib/jvm/java-openjdk

# Install packages, download and extract GlassFish
# Setup password file
# Enable DAS
RUN yum -y install unzip java-1.8.0-openjdk-devel && \
    curl -O $GLASSFISH_URL && \
    echo "$MD5 *$GLASSFISH_PKG" | md5sum -c - && \
    unzip -o $GLASSFISH_PKG && \
    rm -f $GLASSFISH_PKG && \
    yum -y remove unzip && \
    yum clean all

COPY docker-entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

# Ports being exposed
EXPOSE 4848 8080 8181 9009

CMD ["asadmin", "start-domain", "-v", "--debug"]
