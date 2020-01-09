## Alpine Plataform   
#FROM microsoft/dotnet:2.2-sdk-alpine AS build-env

## Debian Plataform   
FROM microsoft/dotnet:2.2-sdk-stretch AS build-env

WORKDIR /app

# copy and build everything else
COPY . ./

##Alpine Plataform
#RUN set -xe \
#    && apk add --update \
#    bash \
#    git \
#    unzip \
#    gnupg \
#    && rm -rf /var/cache/apk/*
  
# Change work directory
WORKDIR Thrust.SCoT.Web

# Package to output directory
RUN dotnet publish -c Release -o out Thrust.SCoT.Web.csproj

# Build da imagem

## Alpine Plataform   
#FROM microsoft/dotnet:2.2-aspnetcore-runtime-alpine

## Debian Plataform   
FROM microsoft/dotnet:2.2-aspnetcore-runtime-stretch-slim

WORKDIR /app

# Binds to ports
EXPOSE  49783

COPY --from=build-env /app/Thrust.SCoT.Web/out .
ENTRYPOINT ["dotnet", "Thrust.SCoT.Web.dll"]