# Build the project
FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
WORKDIR app/
# Copy solution and projects and restore as distinct layers
COPY *.sln .
COPY Engine/Engine.csproj Engine/
COPY LibCommands/LibCommands.csproj LibCommands/
RUN dotnet restore
# Copy everything else and publish
COPY . .
RUN dotnet publish -c Release -o out

# Create project image
FROM mcr.microsoft.com/dotnet/core/runtime:2.2
WORKDIR app/
COPY --from=build-env app/Engine/out .
ENTRYPOINT ["dotnet", "Engine.dll"]