FROM mcr.microsoft.com/dotnet/core/sdk:2.1 AS base
MAINTAINER Daniel NGUYEN

RUN apt-get -y update      
RUN apt-get -y install zip

# Install Python 3.x and Pip
RUN apt-get update && \
    apt-get install python-pip -y

# Install AWS CLI
RUN pip install awscli --upgrade

RUN apt-get update && \
    apt-get install python3 python3-pip -y
