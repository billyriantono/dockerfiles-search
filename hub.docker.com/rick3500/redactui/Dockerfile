FROM mcr.microsoft.com/dotnet/core/runtime:3.0-buster-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["RedactUI/RedactUI.csproj", "RedactUI/"]
COPY ["Redact/RedactCommon.csproj", "Redact/"]
RUN dotnet restore "RedactUI/RedactUI.csproj"
COPY . .
WORKDIR "/src/RedactUI"
RUN dotnet build "RedactUI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RedactUI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RedactUI.dll"]
CMD []
