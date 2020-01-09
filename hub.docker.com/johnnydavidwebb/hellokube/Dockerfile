FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["HelloKube.Web/HelloKube.Web.csproj", "HelloKube.Web/"]
RUN dotnet restore "HelloKube.Web/HelloKube.Web.csproj"
COPY . .
WORKDIR "/src/HelloKube.Web"
RUN dotnet build "HelloKube.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HelloKube.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HelloKube.Web.dll"]