FROM circleci/golang:1.11.4-stretch
USER root
RUN apt-get update && apt-get install -y xz-utils
# Clean up
RUN apt-get clean all && rm -rf /var/lib/apt/lists/*
