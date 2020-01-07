FROM mcr.microsoft.com/dotnet/core-nightly/sdk:3.0-disco AS build
RUN curl -sL https://deb.nodesource.com/setup_10.x |  bash -
RUN apt-get install -y nodejs
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata
ENV TZ=Europe/Berlin
RUN npm install -g --unsafe-perm node-sass core-js core-js-pure date-fns