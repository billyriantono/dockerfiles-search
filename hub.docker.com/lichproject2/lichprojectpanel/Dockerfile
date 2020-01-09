#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["LichProjectPanelSPA/Server/LichProjectPanelSPA.Server.csproj", "LichProjectPanelSPA/Server/"]
COPY ["LichProjectPanelSPA/Client/LichProjectPanelSPA.Client.csproj", "LichProjectPanelSPA/Client/"]
COPY ["LichProjectPanelSPA/Shared/LichProjectPanelSPA.Shared.csproj", "LichProjectPanelSPA/Shared/"]
RUN dotnet restore "LichProjectPanelSPA/Server/LichProjectPanelSPA.Server.csproj"
COPY . .
WORKDIR "/src/LichProjectPanelSPA/Server"
RUN dotnet build "LichProjectPanelSPA.Server.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LichProjectPanelSPA.Server.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LichProjectPanelSPA.Server.dll"]