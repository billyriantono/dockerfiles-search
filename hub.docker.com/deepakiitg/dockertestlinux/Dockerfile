FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 2426
EXPOSE 44347

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /
COPY DockerTestLinux/DockerTestLinux.csproj DockerTestLinux/
RUN dotnet restore DockerTestLinux/DockerTestLinux.csproj
COPY . .
WORKDIR /DockerTestLinux
RUN dotnet build DockerTestLinux.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish DockerTestLinux.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerTestLinux.dll"]
