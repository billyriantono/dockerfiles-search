FROM microsoft/dotnet:2.2.0-aspnetcore-runtime AS base
WORKDIR /app

FROM microsoft/dotnet:2.2.100-sdk AS publish
WORKDIR /src
COPY /src .
WORKDIR /src/Easynovation.Goals.Api
RUN dotnet publish -c Release -o /app

FROM base as final
WORKDIR /app
COPY --from=publish  /app .
EXPOSE 80   
ENTRYPOINT ["dotnet", "Easynovation.Goals.Api.dll"]