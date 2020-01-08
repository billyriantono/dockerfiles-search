#####################################################
# Dockerfile to customeize NODE for GitLab Deployment
# Based on the official NODE
#####################################################

# Set the base image
FROM        node:alpine

# File Author / Maintainer
LABEL       maintainer=vetosers@gmail.com

# Change System TimeZone to Asia/Bangkok
RUN         ln -sf /usr/share/zoneinfo/Asia/Bangkok /etc/localtime

# Install Dependencies
RUN         npm install -g npm \
                grunt-cli \
                yarn \
                express \
                https \
                fs \
                socket.io
