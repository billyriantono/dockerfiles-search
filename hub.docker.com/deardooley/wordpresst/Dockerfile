FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY src/DeadInsect.ApiGateway.csproj src/
RUN dotnet restore src/DeadInsect.ApiGateway.csproj
COPY . .
WORKDIR /src/src
RUN dotnet build DeadInsect.ApiGateway.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish DeadInsect.ApiGateway.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DeadInsect.ApiGateway.dll"]
