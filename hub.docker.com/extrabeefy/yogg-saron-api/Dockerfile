FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["yogg-saron-api.csproj", ""]
RUN dotnet restore "yogg-saron-api.csproj"
COPY . .
WORKDIR "/src/"
RUN dotnet build "yogg-saron-api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "yogg-saron-api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "yogg-saron-api.dll"]

