FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
WORKDIR /app

ENV ASPNETCORE_URLS http://+:5000
EXPOSE 5000

# Copy csproj and restore as distinct layers
# Copy everything and build
COPY . ./

RUN dotnet restore "./tips-web-api.csproj"
RUN dotnet publish "tips-web-api.csproj" -c Release -o out


# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "tips-web-api.dll"]