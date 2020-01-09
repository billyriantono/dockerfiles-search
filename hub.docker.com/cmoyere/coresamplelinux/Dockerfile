FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["CoreSampleLinux/CoreSampleLinux.csproj", "CoreSampleLinux/"]
RUN dotnet restore "CoreSampleLinux/CoreSampleLinux.csproj"
COPY . .
WORKDIR "/src/CoreSampleLinux"
RUN dotnet build "CoreSampleLinux.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CoreSampleLinux.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CoreSampleLinux.dll"]