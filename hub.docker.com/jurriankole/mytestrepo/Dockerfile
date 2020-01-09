FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["myDockerApp.csproj", ""]
RUN dotnet restore "./myDockerApp.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "myDockerApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "myDockerApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "myDockerApp.dll"]