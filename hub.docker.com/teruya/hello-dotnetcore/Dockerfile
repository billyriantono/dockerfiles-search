FROM microsoft/dotnet:1.0.0-core

RUN mkdir -p /dotnetapp
WORKDIR /dotnetapp

COPY app/ .

ENTRYPOINT ["dotnet", "hello-dot-net-core.dll"]
