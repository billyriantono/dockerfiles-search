FROM microsoft/dotnet:2.1-aspnetcore-runtime-bionic AS base
WORKDIR /app
EXPOSE 50393
EXPOSE 44387

FROM microsoft/dotnet:2.1-sdk-bionic AS build
WORKDIR /src
COPY DockerApp/DockerApp.csproj DockerApp/
RUN dotnet restore DockerApp/DockerApp.csproj
COPY . .
WORKDIR /src/DockerApp
RUN dotnet build DockerApp.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish DockerApp.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerApp.dll"]
