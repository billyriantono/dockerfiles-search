FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /src
COPY ["GS.Authentication/GS.Authentication.csproj", "GS.Authentication/"]

RUN dotnet restore "GS.Authentication/GS.Authentication.csproj"
COPY . .
WORKDIR "/src/GS.Authentication"

RUN dotnet build "GS.Authentication.csproj" -c Release -f netcoreapp2.2 -o /app

FROM build AS publish
RUN dotnet publish "GS.Authentication.csproj" -c Release -f netcoreapp2.2 -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "GS.Authentication.dll"]-f netcoreapp2.2