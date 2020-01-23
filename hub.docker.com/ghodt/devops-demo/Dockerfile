FROM ubuntu:16.04

MAINTAINER Sara Ersson "sara.ersson@gmail.com"

# Install python, git, and vim
RUN apt-get update -y && \
    apt-get install -y python-pip python-dev && \
    apt-get install -y git && \
    apt-get install -y vim

# Install Flask 
RUN pip install Flask

# Install pytest
RUN pip install pytest

# Expose port 5000 in the container
EXPOSE 5000
