FROM microsoft/dotnet:2.1-runtime AS base
WORKDIR /app

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY . Braveheart.Orchestrator/
WORKDIR /src/Braveheart.Orchestrator
RUN dotnet restore Braveheart.Orchestrator.sln
COPY . .
RUN dotnet build Braveheart.Orchestrator.sln -c Release -o /app

FROM build AS publish
RUN dotnet publish Braveheart.Orchestrator/Braveheart.Orchestrator.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Braveheart.Orchestrator.dll"]
