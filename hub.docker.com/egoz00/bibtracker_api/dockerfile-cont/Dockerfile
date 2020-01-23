FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 64060
EXPOSE 44389

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY joseph2018/joseph2018.csproj joseph2018/
RUN dotnet restore joseph2018/joseph2018.csproj
COPY . .
WORKDIR /src/joseph2018
RUN dotnet build joseph2018.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish joseph2018.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "joseph2018.dll"]
