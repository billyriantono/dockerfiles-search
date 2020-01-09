FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY CastleWebBackend/CastleWebBackend.csproj CastleWebBackend/
RUN dotnet restore CastleWebBackend/CastleWebBackend.csproj
COPY . .
WORKDIR /src/CastleWebBackend
RUN dotnet build CastleWebBackend.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish CastleWebBackend.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CastleWebBackend.dll"]
