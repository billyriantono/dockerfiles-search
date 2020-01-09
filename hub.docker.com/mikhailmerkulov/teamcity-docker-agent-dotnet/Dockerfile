
FROM mikhailmerkulov/teamcity-docker-agent-cloud

LABEL maintainer "Mikhail Merkulov <mikhail.merkulov@itomy.ch>"

RUN curl -SL https://download.microsoft.com/download/8/A/7/8A765126-50CA-4C6F-890B-19AE47961E4B/dotnet-sdk-2.1.402-linux-x64.tar.gz --output dotnet.tar.gz && mkdir -p /usr/share/dotnet && tar -zxf dotnet.tar.gz -C /usr/share/dotnet && rm dotnet.tar.gz
