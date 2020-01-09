FROM microsoft/dotnet:2.1-sdk-alpine AS build-env
WORKDIR /app

# copy and build everything else
COPY . ./
WORKDIR Thrust.SCooB.Integrations.Agent.Mongo.DeleteCollection

RUN dotnet publish -c Release -o out Thrust.SCooB.Integrations.Agent.Mongo.DeleteCollection.csproj

# Build da imagem
FROM microsoft/dotnet:2.1-runtime-alpine
WORKDIR /app

COPY --from=build-env /app/Thrust.SCooB.Integrations.Agent.Mongo.DeleteCollection/out .
ENTRYPOINT ["dotnet", "Thrust.SCooB.Integrations.Agent.Mongo.DeleteCollection.dll"]