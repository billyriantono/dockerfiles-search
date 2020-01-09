FROM microsoft/dotnet:2.1-sdk-alpine AS build-env
WORKDIR /app

# copy and build everything else
COPY . ./
WORKDIR Thrust.SCooB.Integrations.Agent.Rest.Get

RUN dotnet publish -c Release -o out Thrust.SCooB.Integrations.Agent.Rest.Get.csproj

# Build da imagem
FROM microsoft/dotnet:2.1-runtime-alpine
WORKDIR /app

COPY --from=build-env /app/Thrust.SCooB.Integrations.Agent.Rest.Get/out .
ENTRYPOINT ["dotnet", "Thrust.SCooB.Integrations.Agent.Rest.Get.dll"]