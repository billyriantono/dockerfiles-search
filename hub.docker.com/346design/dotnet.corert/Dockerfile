FROM microsoft/dotnet:3.0-sdk-bionic

LABEL maintainer="346.design"

RUN apt-get update \
 && apt-get upgrade -y \
 && apt-get install -y software-properties-common \
 && add-apt-repository universe \
 && apt-get update \
 && apt-get install -y zsh clang libcurl4-openssl-dev zlib1g-dev libkrb5-dev \
 && apt-get autoremove -y
