FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Docker-Swagger/Docker-Swagger.csproj", "Docker-Swagger/"]
RUN dotnet restore "Docker-Swagger/Docker-Swagger.csproj"
COPY . .
WORKDIR "/src/Docker-Swagger"
RUN dotnet build "Docker-Swagger.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Docker-Swagger.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Docker-Swagger.dll"]