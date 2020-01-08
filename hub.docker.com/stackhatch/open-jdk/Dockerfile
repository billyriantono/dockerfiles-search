# Instruction defines a varibale that users can pass at build-time
ARG base_image_name=stackhatch/centos
ARG base_image_tag=latest

# Specifies the base image from which you are building
FROM $base_image_name:$base_image_tag

# Specifying image meta data for user refernce
LABEL vendor="Stackhatch, Inc" \
      org.stackhatch.image.is-name="open-jdk" \
      org.stackhatch.image.is-version="v1.0.1" \
      org.stackhatch.image.is-maintainer="nanimineni" \
      org.stackhatch.image.is-maintainer.email="nanimineni@stackhatch.org" \
      org.stackhatch.image.is-support.email="support@stackhatch.org" \
      org.stackhatch.image.is-description="Stackhatch, Inc Docker Image for OpenJDK"

# Install Java throguh YUM 
RUN yum  install java -y

# Setting up Java_Home in Environment.
ENV JAVA_HOME /usr/bin/java

