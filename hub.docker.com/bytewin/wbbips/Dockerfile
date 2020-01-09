FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.sln .
COPY bips/*.csproj ./bips/
RUN dotnet restore

# copy everything else and build app
COPY bips/. ./bips/
WORKDIR /app/bips
RUN dotnet publish -c Release -o out


FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS runtime
WORKDIR /app
COPY --from=build /app/bips/out ./
ENTRYPOINT ["dotnet", "bips.dll"]
