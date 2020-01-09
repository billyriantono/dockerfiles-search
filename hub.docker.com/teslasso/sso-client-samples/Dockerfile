FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /src
COPY ["samples/MvcWebAppSample/MvcWebAppSample.csproj", "samples/MvcWebAppSample/"]
COPY ["samples/TeslaSso.Samples.Infrastructure/TeslaSso.Samples.Infrastructure.csproj", "samples/TeslaSso.Samples.Infrastructure/"]
COPY ["src/TeslaSso.SharedCustomizations/TeslaSso.SharedCustomizations.csproj", "src/TeslaSso.SharedCustomizations/"]
RUN dotnet restore "samples/MvcWebAppSample/MvcWebAppSample.csproj"
COPY . .
WORKDIR "/src/samples/MvcWebAppSample"
ARG VERSION=0.9.1-dev
RUN dotnet build "MvcWebAppSample.csproj" -c Release /p:Version=$VERSION

FROM build AS publish
RUN dotnet publish "MvcWebAppSample.csproj" -c Release --no-restore --no-build -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MvcWebAppSample.dll"]