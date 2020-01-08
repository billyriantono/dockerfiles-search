FROM microsoft/dotnet:sdk AS build-env
WORKDIR /app

# copy csproj and restore as distinct layers
COPY src/*.csproj ./
RUN export DOTNET_CLI_TELEMETRY_OPTOUT=0
RUN dotnet restore

# copy everything else and build
COPY src/ ./
RUN dotnet publish -c Release -o out

# build runtime image
FROM microsoft/dotnet:runtime
WORKDIR /app
VOLUME ["/app"]
COPY --from=build-env /app/out ./
COPY go.sh ./
ENTRYPOINT ["/app/go.sh"]
