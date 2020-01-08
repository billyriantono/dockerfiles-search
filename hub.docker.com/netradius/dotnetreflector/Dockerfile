FROM microsoft/dotnet:sdk AS build-env
WORKDIR /app

COPY *.csproj ./
RUN dotnet restore

COPY . ./
RUN dotnet publish -c Release -o out

FROM microsoft/dotnet:aspnetcore-runtime
WORKDIR /app
COPY --from=build-env /app/out .
EXPOSE 8080
HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3 CMD curl --fail http://localhost:8080 || exit 1
ENV ASPNETCORE_URLS "http://*:8080"
ENTRYPOINT ["dotnet", "dotnetreflector.dll"]
# After building you can execute
# docker run -d -p 8080:8080 --name test netradius/dotnetreflector:latest