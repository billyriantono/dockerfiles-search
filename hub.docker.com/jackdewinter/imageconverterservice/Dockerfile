FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["ImageConverter.Service/ImageConverter.Service.csproj", "ImageConverter.Service/"]
RUN dotnet restore "ImageConverter.Service/ImageConverter.Service.csproj"
COPY . .
WORKDIR "/src/ImageConverter.Service"
RUN dotnet build "ImageConverter.Service.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ImageConverter.Service.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ImageConverter.Service.dll"]