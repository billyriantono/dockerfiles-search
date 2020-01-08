#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["MCRoll/MCRoll.csproj", "MCRoll/"]
COPY ["MCRoll.Data/MCRoll.Data.csproj", "MCRoll.Data/"]
COPY ["MCRoll.Model/MCRoll.Model.csproj", "MCRoll.Model/"]
COPY ["MCRoll.ServiceImp/MCRoll.ServiceImp.csproj", "MCRoll.ServiceImp/"]
COPY ["MCRoll.ServiceInterface/MCRoll.ServiceInterface.csproj", "MCRoll.ServiceInterface/"]
RUN dotnet restore "MCRoll/MCRoll.csproj"
COPY . .
WORKDIR "/src/MCRoll"
RUN dotnet build "MCRoll.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MCRoll.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MCRoll.dll"]