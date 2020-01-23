FROM microsoft/aspnetcore-build:2.0.0 AS builder

ADD BootstrapNetCore /BootstrapNetCore

WORKDIR /BootstrapNetCore

RUN dotnet restore DevExpress.AspNetCore.Bootstrap.Starter.csproj -s https://nuget.devexpress.com/early-access/api -s https://api.nuget.org/v3/index.json

RUN dotnet publish DevExpress.AspNetCore.Bootstrap.Starter.csproj --output /app/ --configuration Release


FROM microsoft/aspnetcore:2.0.0

WORKDIR /app

COPY --from=builder /app .

# ENTRYPOINT ["dotnet", "DevExpress.AspNetCore.Bootstrap.Starter.dll"]