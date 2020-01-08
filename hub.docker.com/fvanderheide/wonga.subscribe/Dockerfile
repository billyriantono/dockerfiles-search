FROM microsoft/dotnet:sdk AS build-env

WORKDIR /build
COPY /Wonga.Subscribe/* ./Wonga.Subscribe/
COPY /Wonga.Subscribe.sln ./
RUN dotnet restore Wonga.Subscribe.sln -s https://api.nuget.org/v3/index.json
RUN dotnet publish Wonga.Subscribe.sln -c Debug -o out

FROM microsoft/dotnet:runtime
WORKDIR /app
COPY --from=build-env /build/Wonga.Subscribe/out ./
ENTRYPOINT ["dotnet", "Wonga.Subscribe.dll" ]
