FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /webAPI
# copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore
# copy everything else and build app
COPY . .
RUN dotnet publish MyFood.MobileAppService.csproj -o out /p:PublishWithAspNetCoreTargetManifest="false" 
# copy
FROM microsoft/dotnet:2.2-aspnetcore-runtime AS runtime
ENV ASPNETCORE_URLS http://*:8080
WORKDIR /webAPI
COPY --from=build /webAPI/out ./
ENTRYPOINT ["dotnet", "MyFood.MobileAppService.dll"]