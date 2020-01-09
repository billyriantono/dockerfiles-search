FROM openjdk:8-jdk

MAINTAINER Thorsten Marx <thorsten.marx1@gmail.com>

# In case someone loses the Dockerfile
RUN rm -rf /etc/Dockerfile
ADD Dockerfile /etc/Dockerfile

# Install packages
RUN apt-get update && \ 
    apt-get update --fix-missing && \ 
    apt-get install -y wget

# Download and install webtools
ENV WEBTOOLS_VERSION 1.10.1
RUN wget https://bintray.com/thmarx/generic/download_file?file_path=${WEBTOOLS_VERSION}/webtools-${WEBTOOLS_VERSION}.tar.gz -O webtools-${WEBTOOLS_VERSION}.tar.gz && \
    tar -xzvf webtools-${WEBTOOLS_VERSION}.tar.gz && \
    rm -rf webtools-${WEBTOOLS_VERSION}.tar.gz && \
    mv webtools-${WEBTOOLS_VERSION} /opt/webtools && \
	echo "33093f1e-edb2-4d9d-80f4-34502d7a24bf:admin:9ece086e9bac491fac5c1d1046ca11d737b92a2b2ebd93f005d7b710110c0a678288166e7fbe796883a4f2e9b3ca9f484f521d0ce464345cc1aec96779149c14:admin" > /opt/webtools/webtools/conf/users.realm && \
	echo "apikey=apikey" >> /opt/webtools/webtools/conf/configuration.properties

# Configure Jetty user and clean up install
RUN useradd webtools && \
    chown -R webtools:webtools /opt/webtools

# Set defaults for docker run
WORKDIR /opt/webtools
CMD ["java", "-jar", "start.jar", "jetty.home=/opt/webtools"]
