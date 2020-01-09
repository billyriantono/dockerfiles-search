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
WORKDIR Thrust.SCooB.BotMap.LayerProvider.Mongo

# Install app dependencies
#RUN npm install

# Package to output directory
RUN dotnet publish -c Release -o out Thrust.SCooB.BotMap.LayerProvider.Mongo.csproj

# Build da imagem
FROM microsoft/dotnet:2.1-aspnetcore-runtime
WORKDIR /app

# Binds to ports
EXPOSE  5002

COPY --from=build-env /app/Thrust.SCooB.BotMap.LayerProvider.Mongo/out .
ENTRYPOINT ["dotnet", "Thrust.SCooB.BotMap.LayerProvider.Mongo.dll"]
