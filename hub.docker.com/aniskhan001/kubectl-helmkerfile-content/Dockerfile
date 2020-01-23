
FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY episodio-01.csproj episodio-01/
RUN dotnet restore episodio-01/episodio-01.csproj
WORKDIR /src/episodio-01
COPY . .
RUN dotnet build episodio-01.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish episodio-01.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "episodio-01.dll"]
