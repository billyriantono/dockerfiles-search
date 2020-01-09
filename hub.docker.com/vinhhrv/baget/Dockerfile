FROM microsoft/aspnetcore-build:2.0.5-2.1.4 AS build-env
WORKDIR /app

COPY src/BaGet/BaGet.csproj ./

RUN dotnet restore BaGet.csproj

RUN dotnet publish -c Release -o out ./src/BaGet

FROM microsoft/aspnetcore:2.0.5
WORKDIR /app
COPY --from=build-env /app/src/BaGet/out .
ENTRYPOINT ["dotnet", "BaGet.dll"]