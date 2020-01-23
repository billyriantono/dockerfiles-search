FROM ubuntu:latest

# Install.
RUN apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y curl git

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

ENTRYPOINT ["git"]

RUN git version
