FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["EMS/EMS.csproj", "EMS/"]
RUN dotnet restore "EMS/EMS.csproj"
COPY . .
WORKDIR "/src/EMS"
RUN dotnet build "EMS.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "EMS.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "EMS.dll"]
