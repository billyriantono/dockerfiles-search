FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
WORKDIR /app
COPY *.csproj ./
COPY . ./
RUN [ "dotnet", "restore" ]

FROM build-env AS publish
RUN [ "dotnet", "publish", "-c", "Release", "-o", "/app" ]



FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS runtime
WORKDIR /app
LABEL Author="Justin Morris"
LABEL Maintainer="app@jrmcomputing.com"
COPY --from=publish /app .
ENTRYPOINT [ "dotnet", "webpasskeeper.dll", "--server.urls", "http://*:80" ]