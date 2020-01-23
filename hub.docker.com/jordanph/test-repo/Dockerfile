FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ["UniversalDrive/UniversalDrive.csproj", "UniversalDrive/"]
COPY ["UniversalDrive.Emails/UniversalDrive.Emails.csproj", "UniversalDrive.Emails/"]
RUN dotnet restore "UniversalDrive/UniversalDrive.csproj"
COPY . .
WORKDIR "/src/UniversalDrive"
RUN dotnet build "UniversalDrive.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "UniversalDrive.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "UniversalDrive.dll"]