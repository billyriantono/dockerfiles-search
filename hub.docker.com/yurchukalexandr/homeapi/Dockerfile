FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /src
COPY ["Home.API/Home.API.csproj", "Home.API/"]
RUN dotnet restore "Home.API/Home.API.csproj"
COPY . .
WORKDIR "/src/Home.API"
RUN dotnet build "Home.API.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Home.API.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Home.API.dll"]