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
WORKDIR "UI-UserInterface.Core"

# Install app dependencies
#RUN npm install

# Package to output directory
RUN dotnet publish -c Release -o out UI-UserInterface.Core.csproj

# Build da imagem
FROM microsoft/dotnet:2.1-aspnetcore-runtime
WORKDIR /app

# Binds to ports
EXPOSE  7001

COPY --from=build-env "/app/UI-UserInterface.Core/out" .
ENTRYPOINT ["dotnet", "UI-UserInterface.Core.dll"]