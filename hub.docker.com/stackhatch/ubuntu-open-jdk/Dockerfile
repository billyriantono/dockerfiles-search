# Instruction defines a varibale that users can pass at build-time
ARG base_image_name=stackhatch/ubuntu
ARG base_image_tag=latest

# Specifies the base image from which you are building
FROM $base_image_name:$base_image_tag

# Specifying image meta data for user refernce
LABEL vendor="Stackhatch, Inc" \
      org.stackhatch.image.is-name="ubuntu-open-jdk" \
      org.stackhatch.image.is-version="v1.0.1" \
      org.stackhatch.image.is-maintainer="jbanimineni" \
      org.stackhatch.image.is-maintainer.email="jbanimineni@stackhatch.org" \
      org.stackhatch.image.is-support.email="support@stackhatch.org" \
      org.stackhatch.image.is-description="Stackhatch, Inc Docker Image for OpenJDK based on Ubuntu"

# Install Java throguh apt-get
RUN /usr/bin/apt-get update && \
    /usr/bin/apt-get install openjdk-8-jre-headless -y && \
    # Removing unwanted & Caching files
    /bin/rm -rf /var/lib/apt/lists/*

