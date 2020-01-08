FROM mcr.microsoft.com/dotnet/core/sdk:3.0-bionic AS base
    RUN apt-get update && \
        apt-get install -y wget && \
        apt-get install -y gnupg2 && \
        wget -qO- https://deb.nodesource.com/setup_10.x | bash - && \
        apt-get install -y build-essential nodejs
WORKDIR /app
EXPOSE 80
EXPOSE 443

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get update && apt-get install -y nodejs

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-bionic AS build
WORKDIR /src
COPY React-dotnetcore.csproj ./
RUN dotnet restore "./React-dotnetcore.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "React-dotnetcore.csproj" -c Release -o /app/build

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get update && apt-get install -y nodejs

FROM build AS publish
RUN dotnet publish "React-dotnetcore.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
EXPOSE 5000/tcp
ENV ASPNETCORE_URLS http://*:5000
ENTRYPOINT ["dotnet", "React-dotnetcore.dll"]
