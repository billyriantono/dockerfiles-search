FROM microsoft/dotnet:1.0.0-preview2-sdk

# Set the Working Directory
WORKDIR /app

# Copy the app
COPY . /app

# Restore NuGet Packages
RUN dotnet restore
