FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["APISerial.csproj", "APISerial/"]
RUN dotnet restore "APISerial/APISerial.csproj"
COPY . .
WORKDIR "/src/APISerial"
COPY . .
RUN dotnet build "APISerial.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "APISerial.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "APISerial.dll"]