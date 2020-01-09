FROM microsoft/dotnet:2.1-sdk-alpine AS build-env
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
    && rm -rf /var/cache/apk/*

# Change work directory
WORKDIR GST.Mobile.WebService

# Install app dependencies
RUN npm install

# Package to output directory
RUN dotnet publish -c Release -o out GST.Mobile.WebService.csproj

# Build da imagem
FROM microsoft/dotnet:2.1-aspnetcore-runtime
WORKDIR /app

# Binds to ports
EXPOSE  7000

COPY --from=build-env /app/GST.Mobile.WebService/out .
ENTRYPOINT ["dotnet", "GST.Mobile.WebService.dll"]