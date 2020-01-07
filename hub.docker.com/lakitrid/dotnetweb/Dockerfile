FROM microsoft/dotnet:1.0.1-sdk-projectjson

RUN curl -sL https://deb.nodesource.com/setup_7.x | bash -
RUN apt-get install -y nodejs build-essential bzip2 libkrb5-dev
RUN npm install -g gulp bower