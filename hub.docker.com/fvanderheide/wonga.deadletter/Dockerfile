FROM microsoft/dotnet:sdk AS build-env

WORKDIR /build
COPY /Wonga.DeadLetter/* ./Wonga.DeadLetter/
COPY /Wonga.DeadLetter.sln ./
RUN dotnet restore Wonga.DeadLetter.sln -s https://api.nuget.org/v3/index.json
RUN dotnet publish Wonga.DeadLetter.sln -c Debug -o out

FROM microsoft/dotnet:runtime
WORKDIR /app
COPY --from=build-env /build/Wonga.DeadLetter/out ./
ENTRYPOINT ["dotnet", "Wonga.DeadLetter.dll" ]
