FROM microsoft/dotnet:2.1-sdk

RUN apt-get update && apt-get install openjdk-8-jdk -y

RUN dotnet tool install --global dotnet-sonarscanner

RUN export PATH=$PATH:$HOME/.dotnet/tools/
