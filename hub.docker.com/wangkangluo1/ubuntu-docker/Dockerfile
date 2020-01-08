FROM ubuntu:14.04

# Maintainer: wangkangluo1@gmail.com
MAINTAINER docker_user wangkangluo1@gmail.com

# Commands to update the image
RUN apt-get update && apt-get install -y software-properties-common && add-apt-repository ppa:git-core/ppa && apt-get update && apt-get install -y git && apt-get install -y tmux

# Commands when creating a new container
