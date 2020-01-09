FROM microsoft/dotnet:sdk AS build-env

WORKDIR /app

COPY *.csproj ./
RUN dotnet restore

COPY . ./
RUN dotnet publish -c Release -o out

FROM microsoft/dotnet:runtime
ENV CONSUMER_PUBLIC CONSUMER_SECRET ACCESS_TOKEN_PUBLIC ACCESS_TOKEN_SECRET STEAM_API_KEY

WORKDIR /app
COPY --from=build-env /app/out .

ENTRYPOINT ["dotnet", "FreeGameIsAFreeGame.dll"]

VOLUME ["/app/storage"]
