FROM mcr.microsoft.com/dotnet/core/aspnet:2.2.5-alpine3.9 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2.300-alpine3.9 AS build
WORKDIR /src
COPY ["SuperBoard.UI/SuperBoard.UI.csproj", ""]
COPY ["SuperBoard.DomainModels/SuperBoard.DomainModels.csproj", "SuperBoard.DomainModels/"]
RUN dotnet restore "SuperBoard.UI.csproj"
COPY . .
WORKDIR "/src/"
RUN dotnet build "SuperBoard.UI.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SuperBoard.UI.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SuperBoard.UI.dll"]