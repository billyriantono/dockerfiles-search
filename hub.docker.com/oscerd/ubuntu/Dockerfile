# Ubuntu Dockerfile
#
# https://github.com/oscerd/ubuntu

# Pull base image.
FROM ubuntu:14.04
MAINTAINER Andrea Cosentino <ancosen1985@yahoo.com>

# Install.
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y build-essential 
RUN apt-get install -y software-properties-common
RUN apt-get install -y htop unzip vim wget make 

# Add files.
ADD files/.bashrc /root/.bashrc

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

# Default command.
CMD ["bash"]
