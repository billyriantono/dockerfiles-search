FROM ubuntu:rolling
MAINTAINER Sven Niehus <sven@niehus.eu>

# apt update
RUN apt-get update

# Prerequisites
RUN apt-get install -y wget apt-transport-https

# Register Microsoft key and feed
RUN wget -q https://packages.microsoft.com/config/ubuntu/18.10/packages-microsoft-prod.deb
RUN dpkg -i packages-microsoft-prod.deb
RUN apt-get update

# Set the locale
RUN apt-get install -y locales 
RUN rm -rf /var/lib/apt-get/lists/*
RUN localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.utf8

# Install git
RUN apt-get install -y git

# Install jdk 11
RUN apt-get install -y openjdk-11-jdk

# Install dotnet
ENV DOTNET_CLI_TELEMETRY_OPTOUT=1
RUN apt-get install -y dotnet-sdk-2.2