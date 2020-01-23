FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["PVA.Web/PVA.Web.csproj", "PVA.Web/"]
COPY ["PVA.EFCore/PVA.EFCore.csproj", "PVA.EFCore/"]
COPY ["PVA.Domain/PVA.Domain.csproj", "PVA.Domain/"]
RUN dotnet restore "PVA.Web/PVA.Web.csproj"
COPY . .
WORKDIR "/src/PVA.Web"
RUN dotnet build "PVA.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "PVA.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "PVA.Web.dll"]