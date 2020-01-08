FROM maven:3-jdk-8
# Set maintainer
LABEL maintainer="Laurens Sion <laurens@sion.info>"

# Update and install rsync
RUN apt-get update -q && \
    DEBIAN_FRONTEND=noninteractive apt-get install -qy rsync make && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* 
