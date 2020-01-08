FROM microsoft/dotnet:2.0-sdk
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# copy and build everything else
COPY . ./
RUN dotnet publish -c Release -o out
ENTRYPOINT ["dotnet", "out/mis-api.dll"]

# FROM microsoft/dotnet:2.0-sdk
# WORKDIR /dotnetapp

# # copy csproj and restore as distinct layers
# COPY ./bin/Docker .
# ENV ASPNETCORE_ENVIRONMENT Docker
# ENV ASPNETCORE_URLS "http://+:5000"
# # copy and build everything else

# ENTRYPOINT dotnet mis-api.dll
