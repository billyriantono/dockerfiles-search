FROM ubuntu:19.04
MAINTAINER "Antonio Garcia-Dominguez" a.garcia-dominguez@aston.ac.uk
WORKDIR /ttc
COPY . .

# Install base packages required to install TTC2019 language environments
RUN apt-get update && apt-get install -y \
    gnupg ca-certificates apt-transport-https wget

# Install TTC2019 language environments
RUN apt-get update -y && \
    apt-get install -y python3 openjdk-11-jdk-headless && \
    wget -q https://packages.microsoft.com/ubuntu/19.04/prod/pool/main/a/aspnetcore-runtime-2.2/aspnetcore-runtime-2.2.6-x64.deb && \
    wget -q https://packages.microsoft.com/ubuntu/19.04/prod/pool/main/d/dotnet-host/dotnet-host-2.2.6-x64.deb && \
    wget -q https://packages.microsoft.com/ubuntu/19.04/prod/pool/main/d/dotnet-hostfxr-2.2/dotnet-hostfxr-2.2.6-x64.deb && \
    wget -q https://packages.microsoft.com/ubuntu/19.04/prod/pool/main/d/dotnet-runtime-2.2/dotnet-runtime-2.2.6-x64.deb && \
    wget -q https://packages.microsoft.com/ubuntu/19.04/prod/pool/main/d/dotnet-runtime-deps-2.2/dotnet-runtime-deps-2.2.6-x64.deb && \
    wget -q https://packages.microsoft.com/ubuntu/19.04/prod/pool/main/d/dotnet-sdk-2.2/dotnet-sdk-2.2.301-x64.deb && \
    apt install -y ./*2.2*.deb 

# Build all TTC2019 solutions
WORKDIR /ttc
RUN scripts/run.py -b

# Run a Bash shell by default
CMD /bin/bash
