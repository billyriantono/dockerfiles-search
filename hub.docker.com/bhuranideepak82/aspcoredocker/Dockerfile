# Build image
FROM microsoft/dotnet:2.0.3-sdk AS builder  
WORKDIR /aspdockerimage 
COPY ASPCoreDocker ./ASPCoreDocker/

# Copy all the csproj files and restore to cache the layer for faster builds
# The dotnet_build.sh script does this anyway, so superfluous, but docker can 
# cache the intermediate images so _much_ faster

RUN dotnet restore ASPCoreDocker/ASPCoreDocker.csproj


RUN dotnet build -c Release  ASPCoreDocker/ASPCoreDocker.csproj --no-restore

RUN dotnet publish ASPCoreDocker/ASPCoreDocker.csproj -c Release -o /dist --no-restore

#Build the app image
FROM microsoft/aspnetcore:2.0.3  
WORKDIR /app  
ENV ASPNETCORE_ENVIRONMENT Local
COPY --from=builder /dist .
ENTRYPOINT ["dotnet", "ASPCoreDocker.dll"]  
