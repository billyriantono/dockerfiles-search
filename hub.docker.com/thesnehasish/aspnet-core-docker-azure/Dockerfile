FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 5000/tcp
ENV ASPNETCORE_URLS http://*:5000

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY *.sln ./
COPY aspnet-core-docker-azure/aspnet-core-docker-azure.csproj aspnet-core-docker-azure/
RUN dotnet restore
COPY . .
WORKDIR /src/aspnet-core-docker-azure
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "aspnet-core-docker-azure.dll"]
