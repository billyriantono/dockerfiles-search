FROM mcr.microsoft.com/dotnet/core/runtime:3.0-buster-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["Mailgun.Core/Mailgun.Core.csproj", "Mailgun.Core/"]
RUN dotnet restore "Mailgun.Core/Mailgun.Core.csproj"
COPY . .
WORKDIR "/src/Mailgun.Core"
RUN dotnet build "Mailgun.Core.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Mailgun.Core.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Mailgun.Core.dll"]