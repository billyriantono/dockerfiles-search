FROM microsoft/dotnet:2.2-sdk
WORKDIR /app

# copy csproj and restore as distinct layers
COPY dotnetcore-docker/*.csproj ./
RUN dotnet restore

# copy and build everything else
COPY dotnetcore-docker ./
RUN dotnet publish -c Release -o out
ENTRYPOINT ["dotnet", "out/dotnetcore-docker.dll"]