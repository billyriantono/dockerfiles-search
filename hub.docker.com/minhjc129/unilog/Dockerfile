FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-alpine3.9 AS base
EXPOSE 80
WORKDIR /app


FROM mcr.microsoft.com/dotnet/core/sdk:2.2-alpine3.9 AS build
WORKDIR /src
COPY ["./UniLog.Api/UniLog.Api.csproj", "UniLog.Api/"]
COPY ["./DataService/DataService.csproj", "DataService/"]
COPY ["./Reso.AuthorizationBase.DbManager/Reso.AuthorizationBase.DbManager.csproj", "Reso.AuthorizationBase.DbManager/"]
RUN dotnet restore "UniLog.Api/UniLog.Api.csproj"
COPY . .
WORKDIR "/src/UniLog.Api"
RUN dotnet build "UniLog.Api.csproj" -c Debug -o /app

FROM build AS publish
RUN dotnet publish "UniLog.Api.csproj" -c Debug -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "UniLog.Api.dll"]