FROM mcr.microsoft.com/dotnet/core/runtime:3.0-buster-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY MANAGE4US.Messaging/MANAGE4US.Messaging.csproj MANAGE4US.Messaging/
RUN dotnet restore "MANAGE4US.Messaging/MANAGE4US.Messaging.csproj"
COPY . .
WORKDIR "/src/MANAGE4US.Messaging"
RUN dotnet build "MANAGE4US.Messaging.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MANAGE4US.Messaging.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MANAGE4US.Messaging.dll"]
