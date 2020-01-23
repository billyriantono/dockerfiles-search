FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY GatechPF/GatechPF.csproj GatechPF/
RUN dotnet restore GatechPF/GatechPF.csproj
COPY . .
WORKDIR /src/GatechPF
RUN dotnet build GatechPF.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish GatechPF.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "GatechPF.dll"]
