# Base image from Ubuntu #
FROM ubuntu:17.10

# Add some labels
LABEL base.image="ubuntu:17.10"
LABEL software="Picard analysis tools"
LABEL software.version="2.18.9"
LABEL maintainer="Mike Smith <msmith@bioneos.com>"

USER root

# Prep container
RUN apt-get update && apt-get install -y wget

# Install OpenJDK 8 JRE
RUN apt-get install -y openjdk-8-jre-headless unzip

# Install Picard jarfile, place in /opt/tools
ENV PICARD_VERSION 2.18.9
RUN mkdir /opt/picard-${PICARD_VERSION} && \
  cd /opt/picard-${PICARD_VERSION} && \
  wget https://github.com/broadinstitute/picard/releases/download/${PICARD_VERSION}/picard.jar

# Write bash script to execute jar file using 'picard'
RUN echo "#! /bin/bash\njava -jar /opt/picard-${PICARD_VERSION}/picard.jar \"\$@\"" \
  > /usr/bin/picard

# Set permissions to execute picard
RUN chmod 755 /usr/bin/picard

# Drop privileges
RUN useradd -m picard
WORKDIR /home/picard
USER picard

# Default command
CMD /bin/bash
