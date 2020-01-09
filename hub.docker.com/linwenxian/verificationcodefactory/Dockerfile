FROM  microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 81
EXPOSE 443

RUN apt-get update \
    && apt-get install -y --no-install-recommends libgdiplus libc6-dev \
    && rm -rf /var/lib/apt/lists/*

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["VerificationCodeFactory.csproj", ""]
RUN dotnet restore "VerificationCodeFactory.csproj"
COPY . .
WORKDIR "/src/"
RUN dotnet build "VerificationCodeFactory.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "VerificationCodeFactory.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "VerificationCodeFactory.dll"]