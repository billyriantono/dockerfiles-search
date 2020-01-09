FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base

WORKDIR /app

COPY ./DockerManual/publish .

ENTRYPOINT ["dotnet", "DockerManual.dll"]