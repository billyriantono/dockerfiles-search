FROM microsoft/dotnet:2.1-sdk-alpine AS build-env
WORKDIR /app

# copy and build everything else
COPY . ./
WORKDIR Thrust.SCooB.Integrations.Agent.Rest.Post

RUN dotnet publish -c Release -o out Thrust.SCooB.Integrations.Agent.Rest.Post.csproj

# Build da imagem
FROM microsoft/dotnet:2.1-runtime-alpine
WORKDIR /app

COPY --from=build-env /app/Thrust.SCooB.Integrations.Agent.Rest.Post/out .
ENTRYPOINT ["dotnet", "Thrust.SCooB.Integrations.Agent.Rest.Post.dll"]