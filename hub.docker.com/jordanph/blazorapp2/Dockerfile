FROM microsoft/dotnet:2.1-sdk-stretch AS builder
WORKDIR /BlazorApp2

COPY *.sln ./
COPY BlazorApp2.App ./BlazorApp2.App
COPY BlazorApp2.Server ./BlazorApp2.Server

RUN dotnet restore

RUN dotnet publish --output /BlazorApp2/ --configuration Release /p:PublishWithAspNetCoreTargetManifest="false"

FROM microsoft/dotnet:2.1.1-aspnetcore-runtime
WORKDIR /BlazorApp2
ENV ASPNETCORE_URLS http://+:5000

COPY --from=builder /BlazorApp2 .

ENTRYPOINT ["dotnet","BlazorApp2.Server.dll"]
