# Derived from aspnet core sdk for build
FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build

# App Directory
WORKDIR /app

# Copy source files
COPY . .

# Restore all dependencies
RUN dotnet restore UniSteelWeb/UniSteelWeb.csproj

# Net core build
RUN dotnet publish UniSteelWeb/UniSteelWeb.csproj -c Release -o out

# Derived from aspnet core runtime
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS runtime

# App Directory
WORKDIR /app

# Copy source files
COPY --from=build /app/UniSteelWeb/out ./

# Setting Environment
ENV ASPNETCORE_ENVIRONMENT=Production

# Run
ENTRYPOINT ["dotnet", "UniSteelWeb.dll"]

# Params
CMD []