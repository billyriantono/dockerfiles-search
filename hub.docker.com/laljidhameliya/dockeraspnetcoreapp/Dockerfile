FROM microsoft/aspnetcore:1.0.1
ENTRYPOINT ["dotnet", "DockerDotnetCoreApp.dll"]
ARG source=.
WORKDIR /app
EXPOSE 5000/tcp
ENV ASPNETCORE_URLS http://*:5000
COPY $source .
