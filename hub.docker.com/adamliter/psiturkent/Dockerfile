FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY CakeBalance.Api/*.csproj ./CakeBalance.Api/
COPY CakeBalance.TrueLayer/*.csproj ./CakeBalance.TrueLayer/
WORKDIR /app/CakeBalance.Api
RUN dotnet restore

# copy and publish app and libraries
WORKDIR /app/
COPY CakeBalance.Api/. ./CakeBalance.Api/
COPY CakeBalance.TrueLayer/. ./CakeBalance.TrueLayer/
WORKDIR /app/CakeBalance.Api
RUN dotnet publish -c Release -o out

EXPOSE 5100

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS runtime
WORKDIR /app
COPY --from=build /app/CakeBalance.Api/out ./
ENTRYPOINT ["dotnet", "CakeBalance.Api.dll"]

