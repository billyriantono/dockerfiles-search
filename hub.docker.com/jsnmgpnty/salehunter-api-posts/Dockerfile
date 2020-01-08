FROM microsoft/dotnet:2.1-sdk AS build-env
WORKDIR /src

# Copy csproj and restore as distinct layers
COPY *.sln .
COPY . .
RUN dotnet restore SaleHunter.sln

# Set environment to release first
ENV ASPNETCORE_ENVIRONMENT Release

# Copy everything else and build
COPY . .
WORKDIR SaleHunter.PostsApi
RUN dotnet publish --output /out/ --configuration Release

# Build runtime image
FROM microsoft/dotnet:2.1-aspnetcore-runtime
WORKDIR /out
COPY --from=build-env /out .
ENTRYPOINT ["dotnet", "SaleHunter.PostsApi.dll"]