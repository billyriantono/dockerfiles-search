FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["Home.SupplyAndDemand.Api/Home.SupplyAndDemand.Api.csproj", "Home.SupplyAndDemand.Api/"]
RUN dotnet restore "Home.SupplyAndDemand.Api/Home.SupplyAndDemand.Api.csproj"
COPY . .
WORKDIR "/src/Home.SupplyAndDemand.Api"
RUN dotnet build "Home.SupplyAndDemand.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Home.SupplyAndDemand.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Home.SupplyAndDemand.Api.dll"]