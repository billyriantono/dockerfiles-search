###################################
# Dockerfile to build a new image
###################################
# Base image is Ubuntu
FROM ubuntu:16.04

# Author
MAINTAINER Erik Babu <erikbabu@gmail.com>

# Create dir and file
RUN mkdir mynewdir
RUN touch /mynewdir/mynewfile

# Write message in file
RUN echo 'this is my new container to make image and push to hub' > /mynewdir/mynewfile
