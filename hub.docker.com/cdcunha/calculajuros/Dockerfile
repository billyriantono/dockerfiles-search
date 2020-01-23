FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["CalculaJuros/CalculaJuros.csproj", "CalculaJuros/"]
RUN dotnet restore "CalculaJuros/CalculaJuros.csproj"
COPY . .
WORKDIR "/src/CalculaJuros"
RUN dotnet build "CalculaJuros.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CalculaJuros.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CalculaJuros.dll"]