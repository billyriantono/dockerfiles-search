FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 as build
WORKDIR /app
ENV NODE_VERSION 8.5.0
COPY *.sln ./
COPY DockerRegistryViewer/DockerRegistryViewer.csproj ./DockerRegistryViewer
COPY DockerRegistryViewerTests/DockerRegistryViewerTests.csproj ./DockerRegistryViewerTests
RUN dotnet restore
COPY . .
WORKDIR ./DockerRegistryViewer
RUN npm install
WORKDIR /app


FROM build as test
WORKDIR ./DockerRegistryViewerTests
RUN dotnet test

FROM build as publish
WORKDIR /app/DockerRegistryViewerHealthChecker
RUN dotnet build -c RELEASE
WORKDIR /app/DockerRegistryViewer
RUN dotnet publish -c RELEASE -o /builtapp

FROM base AS production
COPY --from=publish /builtapp .
COPY --from=publish /app/DockerRegistryViewerHealthChecker/bin/RELEASE/netcoreapp2.0/ ./health/
HEALTHCHECK --interval=1m --timeout=10s --start-period=5s --retries=1 CMD [ "dotnet", "./health/DockerRegistryViewerHealthChecker.dll" ]
ENTRYPOINT [ "dotnet", "DockerRegistryViewer.dll" ]