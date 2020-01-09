FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /src
COPY . .
RUN dotnet restore "ultra-dashboard-bot.csproj"
RUN dotnet build "ultra-dashboard-bot.csproj" -c Release -o /app
RUN dotnet publish "ultra-dashboard-bot.csproj" -c Release -o /app

FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "ultra-dashboard-bot.dll"]