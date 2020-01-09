FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["REST.net/REST.net.csproj", "REST.net/"]
RUN dotnet restore "REST.net/REST.net.csproj"
COPY . .
WORKDIR "/src/REST.net"
RUN dotnet build "REST.net.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "REST.net.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "REST.net.dll"]