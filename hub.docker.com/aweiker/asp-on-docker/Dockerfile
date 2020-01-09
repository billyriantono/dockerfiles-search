FROM microsoft/aspnetcore-build:2.0 AS build-env
WORKDIR /demo
# Copy csproj and restore as distinct layers
COPY . ./
RUN dotnet restore
# RUN dotnet test

# Copy everything else and build
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/aspnetcore:2.0

WORKDIR /demo

COPY --from=build-env /demo/out .
ENTRYPOINT ["dotnet", "presentation.dll"]