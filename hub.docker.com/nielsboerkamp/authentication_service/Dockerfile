FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY AuthenticationService/AuthenticationService.csproj AuthenticationService/
COPY AuthenticationService.DataLayer/AuthenticationService.DataLayer.csproj AuthenticationService.DataLayer/
COPY AuthenticationService.BusinessLayer/AuthenticationService.BusinessLayer.csproj AuthenticationService.BusinessLayer/
COPY AuthenticationService.Api/AuthenticationService.Api.csproj AuthenticationService.Api/
COPY AuthenticationService.Security/AuthenticationService.Security.csproj AuthenticationService.Security/
RUN dotnet restore AuthenticationService/AuthenticationService.csproj
COPY . .
WORKDIR /src/AuthenticationService
RUN dotnet build AuthenticationService.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish AuthenticationService.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AuthenticationService.dll"]
