FROM microsoft/dotnet:2.1-sdk-alpine AS build-env
WORKDIR /app

# copy and build everything else
COPY . ./
WORKDIR Thrust.SCooB.Agents.MediaClassifier

RUN dotnet publish -c Release -o out Thrust.SCooB.Agents.MediaClassifier.csproj

# Build da imagem
FROM microsoft/dotnet:2.1-runtime-alpine
WORKDIR /app

COPY --from=build-env /app/Thrust.SCooB.Agents.MediaClassifier/out .
ENTRYPOINT ["dotnet", "Thrust.SCooB.Agents.MediaClassifier.dll"]