FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["APIDocker.csproj", "APIDocker/"]
RUN dotnet restore "APIDocker/APIDocker.csproj"
WORKDIR "/src/APIDocker"
COPY . .
RUN dotnet build "APIDocker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "APIDocker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "APIDocker.dll"]