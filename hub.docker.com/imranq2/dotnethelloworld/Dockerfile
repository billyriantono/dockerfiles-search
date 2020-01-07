FROM microsoft/dotnet:latest
# FROM microsoft/dotnet:1.0-runtime
COPY . /app
WORKDIR /app
 
RUN ["dotnet", "restore"]
RUN ["dotnet", "build"]

ENTRYPOINT ["dotnet", "run"]
