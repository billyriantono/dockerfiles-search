FROM microsoft/dotnet:sdk AS build-env

WORKDIR /build
COPY /Wonga.Publish/* ./Wonga.Publish/
COPY /Wonga.Publish.sln ./
RUN dotnet restore Wonga.Publish.sln -s https://api.nuget.org/v3/index.json
RUN dotnet publish Wonga.Publish.sln -c Debug -o out

FROM microsoft/dotnet:runtime
WORKDIR /app
COPY --from=build-env /build/Wonga.Publish/out ./
ENTRYPOINT ["dotnet", "Wonga.Publish.dll" ]
