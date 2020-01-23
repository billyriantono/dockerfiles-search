
FROM microsoft/dotnet:1.1.1-sdk

COPY ./src/FreeLancer.Auth/FreeLancer.Auth.csproj /app/
COPY ./NuGet.Config /app/
WORKDIR /app/
RUN dotnet restore

ADD ./src/FreeLancer.Auth/ /app/
RUN dotnet publish -c Debug -o out

EXPOSE 5000
ENTRYPOINT ["dotnet", "out/FreeLancer.Auth.dll"]