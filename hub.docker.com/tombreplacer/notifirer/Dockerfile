FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /app
COPY src/ ./src
COPY *.sln .
RUN dotnet publish ./src/App.Web/App.Web.csproj -c release --runtime linux-x64 -o /app/out /p:PublishWithAspNetCoreTargetManifest="false"

FROM microsoft/dotnet:2.2-aspnetcore-runtime 
WORKDIR /app
COPY --from=build /app/out ./
RUN ls -al > 1.txt
EXPOSE 5000
ENTRYPOINT ["dotnet", "/app/App.Web.dll"]
