FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim-arm32v7 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["GInfo.Web/GInfo.Web.csproj", "GInfo.Web/"]
RUN dotnet restore "GInfo.Web/GInfo.Web.csproj"
COPY . .
WORKDIR "/src/GInfo.Web"
RUN dotnet build "GInfo.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "GInfo.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "GInfo.Web.dll"]