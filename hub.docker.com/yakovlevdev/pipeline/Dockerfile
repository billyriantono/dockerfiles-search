FROM microsoft/dotnet:2.2-sdk AS build-env

# BEGIN MODIFICATION - Node is needed for development (but not production)
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -y nodejs
# END MODIFICATION

WORKDIR /sln

# copy solution
COPY *.sln ./


# Copy csproj and restore as distinct layers
COPY ./CommonLib/*.csproj ./CommonLib/
COPY ./Pipeline/*.csproj ./Pipeline/
RUN dotnet restore

# Copy everything else and build
COPY ./CommonLib ./CommonLib
COPY ./Pipeline ./Pipeline

RUN dotnet publish "./Pipeline/Pipeline.csproj" -c Release -o /out

COPY ./Pipeline/pipeline.dev.db /out

# Build runtime image
FROM microsoft/dotnet:2.2-aspnetcore-runtime
WORKDIR /app
COPY --from=build-env /out .
ENTRYPOINT ["dotnet", "Pipeline.dll"]