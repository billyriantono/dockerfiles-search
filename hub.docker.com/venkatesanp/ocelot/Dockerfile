FROM microsoft/dotnet:sdk AS build-env
COPY . Gateway
WORKDIR Gateway
WORKDIR Gateway
RUN dotnet restore
RUN dotnet publish -c release -o artificat
FROM microsoft/dotnet:aspnetcore-runtime
WORKDIR /app
COPY --from=build-env /Gateway/Gateway/artificat .
ENTRYPOINT ["dotnet", "Gateway.dll"]