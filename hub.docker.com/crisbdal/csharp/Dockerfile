FROM ubuntu:xenial

RUN apt-get update \
    && sh -c 'echo "deb https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' \
    && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893 \
    && apt-get install  -y apt-transport-https \
    && apt-get update

RUN apt-get install -y dotnet-dev-1.0.0-preview2.1-003177 && dotnet help

ADD . /app
WORKDIR /app

RUN dotnet restore && dotnet build ./*/project.json
CMD tar -czf - .
