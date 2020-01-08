FROM ubuntu:latest
RUN apt-get update
RUN apt-get install -y wget && \
    wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb && \
    dpkg -i packages-microsoft-prod.deb && \
    apt-get update && \
    apt-get install -y aspnetcore-runtime-3.0 && \
    apt-get install -y powershell
