FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["Src/HackMe.challenge/", "HackMe.challenge/"]
RUN dotnet restore "HackMe.challenge/HackMe.challenge.csproj"
# COPY . .
WORKDIR "/src/HackMe.challenge"
RUN dotnet build "HackMe.challenge.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HackMe.challenge.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HackMe.challenge.dll"]