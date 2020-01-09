FROM microsoft/dotnet:2.2.0-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Albelli.Api/Albelli.Api.csproj", "Albelli.Api/"]
COPY ["Albelli.Model/Albelli.Model.csproj", "Albelli.Model/"]
COPY ["Albelli.Services/Albelli.Services.csproj", "Services.Api/"]
RUN dotnet restore "Albelli.Api/Albelli.Api.csproj"
COPY . .
WORKDIR "/src/Albelli.Api"
RUN dotnet build "Albelli.Api.csproj" -c Release -o /app
RUN dotnet test

FROM build AS publish
RUN dotnet publish "Albelli.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Albelli.Api.dll"]