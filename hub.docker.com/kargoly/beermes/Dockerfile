FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["MES/MES.csproj", "MES/"]
COPY ["Messages/Messages.csproj", "Messages/"]
COPY ["DataModel/DataModel.csproj", "DataModel/"]

RUN dotnet restore "MES/MES.csproj"
RUN dotnet restore "Messages/Messages.csproj"
RUN dotnet restore "DataModel/DataModel.csproj"


COPY . .
WORKDIR "/src/MES"
RUN dotnet build "MES.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MES.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MES.dll"]