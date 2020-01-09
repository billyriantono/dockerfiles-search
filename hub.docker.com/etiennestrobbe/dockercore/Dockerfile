FROM microsoft/dotnet:2.1-sdk

WORKDIR /app
COPY Program.cs .
COPY ConsoleApp.csproj .
RUN dotnet restore
RUN dotnet publish

ENTRYPOINT ["dotnet", "ConsoleApp.dll"]