FROM microsoft/dotnet:2.1.300-sdk AS build

WORKDIR /code

COPY . .

RUN dotnet restore

RUN dotnet publish Webservices/Webservices.csproj --output /output --configuration Release

FROM microsoft/dotnet:2.1-aspnetcore-runtime

COPY --from=build /output /app

WORKDIR /app

ENTRYPOINT ["dotnet", "Webservices.dll"]