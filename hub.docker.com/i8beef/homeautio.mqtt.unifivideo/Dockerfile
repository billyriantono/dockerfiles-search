FROM microsoft/dotnet:2.1-sdk-alpine AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY nuget.config .
COPY *.sln .
COPY HomeAutio.Mqtt.UnifiVideo/*.csproj ./HomeAutio.Mqtt.UnifiVideo/
RUN dotnet restore

# copy and build everything else
COPY HomeAutio.Mqtt.UnifiVideo/. ./HomeAutio.Mqtt.UnifiVideo/
RUN dotnet build -c Release

# publish
FROM build AS publish
WORKDIR /app/HomeAutio.Mqtt.UnifiVideo
RUN dotnet publish -o out

# build runtime image
FROM microsoft/dotnet:2.1-runtime-alpine AS runtime
WORKDIR /app
COPY --from=publish /app/HomeAutio.Mqtt.UnifiVideo/out ./

ENV ENVIRONMENT Production

VOLUME ["/app/appsettings.Production.json", "/app/logs"]
ENTRYPOINT ["dotnet", "HomeAutio.Mqtt.UnifiVideo.dll"]