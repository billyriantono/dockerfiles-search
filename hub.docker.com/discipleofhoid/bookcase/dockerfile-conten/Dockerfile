FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 5000

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ./LinuxDockerTest.csproj ./LinuxDockerTest.csproj
RUN dotnet restore 
COPY . .
WORKDIR /src
RUN dotnet build LinuxDockerTest.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish LinuxDockerTest.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "LinuxDockerTest.dll"]
