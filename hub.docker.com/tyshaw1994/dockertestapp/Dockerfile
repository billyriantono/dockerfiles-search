FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 3909
EXPOSE 44338

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["DockerTestApp/DockerTestApp.csproj", "DockerTestApp/"]
RUN dotnet restore "DockerTestApp/DockerTestApp.csproj"
COPY . .
WORKDIR "/src/DockerTestApp"
RUN dotnet build "DockerTestApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DockerTestApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerTestApp.dll"]