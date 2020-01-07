# Base image
# FROM docker.io/ubuntu:16.04
FROM python:3.6-slim

# Install python3 and any other tools
RUN apt-get update && apt-get update && apt-get install -y --no-install-recommends \
    unzip \
    libaio1 \
	&& apt-get clean && rm -rf /var/lib/apt/lists/*

# Add install files
COPY install /tmp

# Set up the Oracle client, remove zip afterwards
RUN mkdir -p /opt/oracle/instantclient-linix && \
    unzip /tmp/instantclient-basic-linux.zip -d /opt/oracle/instantclient-linix && \
    rm /tmp/instantclient-basic-linux.zip
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/oracle/instantclient-linix/instantclient_18_3

# Run pip install to install python packages
RUN pip3 install --upgrade pip -r /tmp/requirements.txt

# Default entrypoint
ENTRYPOINT [ "sh" ]