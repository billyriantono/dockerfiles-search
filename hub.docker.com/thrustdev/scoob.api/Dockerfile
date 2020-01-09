# Alpine Plataform   
FROM microsoft/dotnet:2.2-sdk-alpine AS build-env

WORKDIR /app

# copy and build everything else
COPY . ./ 

RUN set -xe \
   && apk add --update \
   bash \
   git \
   unzip \
   gnupg \
   nodejs\
   nodejs-npm\
   && rm -rf /var/cache/apk/*

# Change work directory
WORKDIR Thrust.SCooB.Api

# Install app dependencies
RUN npm install

# Package to output directory
RUN dotnet publish -c Release -o out Thrust.SCooB.Api.csproj

# Build da imagem
FROM microsoft/dotnet:2.2-aspnetcore-runtime-alpine

WORKDIR /app

# install libgdiplus
RUN apk add libgdiplus --no-cache --repository http://dl-4.alpinelinux.org/alpine/edge/testing

# Binds to ports
EXPOSE  5000

COPY --from=build-env /app/Thrust.SCooB.Api/out .
ENTRYPOINT ["dotnet", "Thrust.SCooB.Api.dll"]
# End Alpine