FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["MinikubeAPI/MinikubeAPI.csproj", "MinikubeAPI/"]
RUN dotnet restore "MinikubeAPI/MinikubeAPI.csproj"
COPY . .
WORKDIR "/src/MinikubeAPI"
RUN dotnet build "MinikubeAPI.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MinikubeAPI.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MinikubeAPI.dll"]