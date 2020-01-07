FROM mcr.microsoft.com/dotnet/core/sdk:2.1
ENV DEBIAN_FRONTEND noninteractive
RUN dotnet tool install -g Amazon.Lambda.Tools
ENV PATH="$PATH:/root/.dotnet/tools"
RUN apt-get update
RUN apt-get install -y zip unzip