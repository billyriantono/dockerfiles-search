FROM microsoft/aspnetcore-build:1.1
ARG source
COPY . /app
WORKDIR /app

RUN ["dotnet", "restore", "/app/DC1/DC1.csproj"]
RUN ["dotnet", "build", "/app/DC1/DC1.csproj"]

EXPOSE 5000/tcp
ENV ASPNETCORE_URLS http://*:5000

ENTRYPOINT ["dotnet", "/app/DC1/bin/Debug/netcoreapp1.1/DC1.dll"]
