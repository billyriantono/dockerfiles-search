FROM microsoft/aspnetcore:2.0 as base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 as builder
WORKDIR /src
COPY *.sln ./
COPY CleverApps.Services.Orders/CleverApps.Services.Orders.csproj CleverApps.Services.Orders/

RUN dotnet restore
COPY . .

WORKDIR /src/CleverApps.Services.Orders
RUN dotnet build -c Release -o /app

FROM builder as publish
RUN dotnet publish --output ./publish

FROM base as production
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT [ "dotnet", "CleverApps.Services.Orders.dll" ]
