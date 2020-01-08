FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-alpine AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-alpine AS build
WORKDIR /src
COPY /src/App/App.csproj ./App/
RUN dotnet restore App/App.csproj
COPY /src .

WORKDIR /src/App
RUN dotnet build App.csproj -c Release -o /app -r linux-arm

FROM build AS publish
RUN dotnet publish App.csproj -c Release -o /app -r linux-arm

# Final image
FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "App.dll"]