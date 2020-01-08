FROM mcr.microsoft.com/dotnet/core/aspnet:3.0
MAINTAINER Krzysztof Kawalec <kf.kawalec@gmail.com>
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        procps \
        telnet \
        iputils-ping \
        nano \
    && apt-get clean \
    && rm -r /var/lib/apt/lists/*
