FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 64426
EXPOSE 44303

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["PingTreePOCAPI.csproj", "PingTreePOCAPI/"]
RUN dotnet restore "PingTreePOCAPI/PingTreePOCAPI.csproj"
COPY . PingTreePOCAPI/
WORKDIR "/src/PingTreePOCAPI"
RUN dotnet build "PingTreePOCAPI.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "PingTreePOCAPI.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "PingTreePOCAPI.dll"]





#FROM microsoft/dotnet:2.1-sdk AS build
#WORKDIR /app
#
## copy csproj and restore as distinct layers
#COPY *.sln .
#COPY PingTreePOCAPI/*.csproj ./PingTreePOCAPI/
#RUN dotnet restore
#
## copy everything else and build app
#COPY PingTreePOCAPI/. ./PingTreePOCAPI/
#WORKDIR /app/PingTreePOCAPI
#RUN dotnet publish -c Release -o out
#
#
#FROM microsoft/dotnet:2.1-aspnetcore-runtime AS runtime
#WORKDIR /app
#COPY --from=build /app/PingTreePOCAPI/out ./
#ENTRYPOINT ["dotnet", "PingTreePOCAPI.dll"]