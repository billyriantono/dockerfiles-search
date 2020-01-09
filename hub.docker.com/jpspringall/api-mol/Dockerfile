FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY . Api.MOL/
WORKDIR /src/Api.MOL
RUN dotnet restore Api.MOL.sln
COPY . .
RUN dotnet build Api.MOL.sln -c Release -o /app

FROM build AS publish
RUN dotnet publish Api.MOL/Api.MOL.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Api.MOL.dll"]
