FROM mcr.microsoft.com/azure-functions/dotnet:2.0

RUN apt-get update \
    && apt-get install wget unzip procps -y \
    && wget https://aka.ms/getvsdbgsh -O - 2>/dev/null | /bin/sh /dev/stdin -v vs2017u5 -l ~/vsdbg