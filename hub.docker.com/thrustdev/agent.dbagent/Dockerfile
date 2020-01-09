FROM microsoft/dotnet:2.1-sdk-alpine AS build-env
WORKDIR /app

# copy and build everything else
COPY . ./
WORKDIR Thrust.SCooB.Agents.DbAgent

RUN dotnet publish -c Release -o out Thrust.SCooB.Agents.DbAgent.csproj

# Build da imagem
FROM microsoft/dotnet:2.1-runtime-alpine
WORKDIR /app

COPY --from=build-env /app/Thrust.SCooB.Agents.DbAgent/out .
ENTRYPOINT ["dotnet", "Thrust.SCooB.Agents.DbAgent.dll"]