FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY . .
RUN dotnet restore ./MyConsoleApp/MyConsoleApp/*.csproj
RUN dotnet restore ./MyConsoleApp/MyConsoleApp.Test/*.csproj

#cope everything else and build app
COPY . .
WORKDIR /app/MyConsoleApp/MyConsoleApp
RUN dotnet build

FROM build AS testrunner
WORKDIR /app/MyConsoleApp/MyConsoleApp.Test
ENTRYPOINT ["dotnet", "test", "--logger:trx"]

FROM build AS test
WORKDIR /app/MyConsoleApp/MyConsoleApp.Test
RUN dotnet test

FROM build AS publish
WORKDIR /app/MyConsoleApp/MyConsoleApp
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/core/runtime:2.2 AS runtime
WORKDIR /app
COPY --from=publish /app/MyConsoleApp/MyConsoleApp/out ./
ENTRYPOINT ["dotnet", "MyConsoleApp.dll"]