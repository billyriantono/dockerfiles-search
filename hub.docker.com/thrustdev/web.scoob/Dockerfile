## Alpine Plataform   
# FROM microsoft/dotnet:2.2-sdk-alpine AS build-env

# WORKDIR /app

# # copy and build everything else
# COPY . ./ 

# RUN set -xe \
#    && apk add --update \
#    bash \
#    git \
#    unzip \
#    gnupg \
#    nodejs\
#    nodejs-npm\
#    && rm -rf /var/cache/apk/*

# # Change work directory
# WORKDIR Thrust.SCooB.Web

# # Install app dependencies
# RUN npm install

# # Package to output directory
# RUN dotnet publish -c Release -o out Thrust.SCooB.Web.csproj

# # Build da imagem
# FROM microsoft/dotnet:2.2-aspnetcore-runtime-alpine

# WORKDIR /app

# # install libgdiplus
# RUN apk add libgdiplus --no-cache --repository http://dl-4.alpinelinux.org/alpine/edge/testing

# # Binds to ports
# EXPOSE  80

# COPY --from=build-env /app/Thrust.SCooB.Web/out .
# ENTRYPOINT ["dotnet", "Thrust.SCooB.Web.dll"]
## End Alpine

## Debian Plataform 
FROM microsoft/dotnet:2.2-sdk-stretch AS build-env

WORKDIR /app

# copy and build everything else
COPY . ./

RUN apt-get -qq update && apt-get -qqy --no-install-recommends install wget gnupg \
    bzip2 \
    git \
    unzip

RUN curl -sL https://deb.nodesource.com/setup_6.x |  bash -
RUN apt-get install -y nodejs

RUN npm i phantomjs-prebuilt

# Change work directory
WORKDIR Thrust.SCooB.Web

# Install app dependencies
RUN npm install

# Package to output directory
RUN dotnet publish -c Release -o out Thrust.SCooB.Web.csproj

# Build da imagem
FROM microsoft/dotnet:2.2-aspnetcore-runtime-stretch-slim

WORKDIR /app

# install libgdiplus
RUN apt-get update
RUN apt-get install -y libgdiplus

# Binds to ports
EXPOSE  80

COPY --from=build-env /app/Thrust.SCooB.Web/out .
COPY --from=build-env /app/Thrust.SCooB.Web/node_modules node_modules

ENTRYPOINT ["dotnet", "Thrust.SCooB.Web.dll"]
## End Debian