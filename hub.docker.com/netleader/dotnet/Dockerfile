FROM microsoft/dotnet:2.2-aspnetcore-runtime AS build
WORKDIR /app

RUN apt-get update
RUN apt-get install -y gnupg
RUN curl -sL https://deb.nodesource.com/setup_11.x -o nodesource_setup.sh
RUN chmod +x nodesource_setup.sh
RUN ./nodesource_setup.sh
RUN apt-get install -y nodejs
RUN apt-get autoclean
RUN rm nodesource_setup.sh
