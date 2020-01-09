FROM microsoft/dotnet:sdk AS builder
WORKDIR /app
COPY ./ ./

# Restore solution packages
RUN dotnet restore BeersAPI.sln

# Build project
RUN dotnet publish BeersAPI/BeersAPI.csproj -c Release -o out

# Build runtime image
FROM microsoft/dotnet:2.2-aspnetcore-runtime
WORKDIR /app
COPY --from=builder /app/BeersAPI/out .

ENTRYPOINT ["dotnet", "BeersAPI.dll"]