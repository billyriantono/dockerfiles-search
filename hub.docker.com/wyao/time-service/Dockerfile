FROM microsoft/dotnet:2.2-sdk AS build-env
WORKDIR /app
COPY . .

WORKDIR /app/time-service
RUN ["dotnet", "restore"]
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/dotnet:2.2-sdk
WORKDIR /app
COPY --from=build-env /app/time-service/out/ .
EXPOSE 5050 80 443
ENTRYPOINT ["dotnet", "time-service.dll"]

