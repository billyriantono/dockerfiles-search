FROM microsoft/dotnet:latest
COPY . /Users/emiljaranilla/Projects/Sample_Vue/Sample_Vue/bin/netcoreapp2.1/Release
WORKDIR /Users/emiljaranilla/Projects/Sample_Vue/Sample_Vue/bin/netcoreapp2.1/Release

EXPOSE 5000/tcp
ENV ASPNETCORE_URLS http://*:5000
ENV ASPNETCORE_ENVIRONMENT docker

ENTRYPOINT dotnet Sample_Vue.dll