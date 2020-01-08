FROM microsoft/dotnet:2.2-sdk

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get update \
    && apt-get install -y nodejs

RUN npm install -g grunt webpack