FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Hello2/Hello2.csproj", "Hello2/"]
RUN dotnet restore "Hello2/Hello2.csproj"
COPY . .
WORKDIR "/src/Hello2"
RUN dotnet build "Hello2.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Hello2.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Hello2.dll"]