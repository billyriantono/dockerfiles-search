FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["refresh-api.csproj", ""]
RUN dotnet restore "refresh-api.csproj"
COPY . .
WORKDIR "/src/"
RUN dotnet build "refresh-api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "refresh-api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "refresh-api.dll"]