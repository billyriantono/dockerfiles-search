############################################################
# Dockerfile to build Ubuntu container images
############################################################

FROM ubuntu:latest

MAINTAINER Varun Vasan V

RUN apt-get update

# Installing Supervisor daemon
RUN apt-get install -y vim inotify-tools supervisor
RUN mkdir -p /var/log/supervisor