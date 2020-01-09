FROM microsoft/aspnetcore-build:2.0 AS build-env
WORKDIR /app

COPY . ./
RUN dotnet restore Miotiq.Billing.Host/*.csproj
RUN dotnet publish Miotiq.Billing.Host/*.csproj -c Release -o out

FROM microsoft/aspnetcore:2.0
WORKDIR /app
COPY --from=build-env /app/Miotiq.Billing.Host/out .
ENTRYPOINT ["dotnet", "Miotiq.Billing.Host.dll"]

