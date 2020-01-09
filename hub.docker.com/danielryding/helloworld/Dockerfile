FROM microsoft/dotnet:1.0.0-preview1

COPY . /dotnetapp
WORKDIR /dotnetapp
RUN dotnet restore
EXPOSE 5000
ENTRYPOINT dotnet run -p /dotnetapp/src/HelloWorld