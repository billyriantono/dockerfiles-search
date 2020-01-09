FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src

COPY . .
WORKDIR /src
RUN dotnet restore
RUN dotnet publish -c Release -o out

FROM microsoft/dotnet:2.1-aspnetcore-runtime
WORKDIR /app
COPY --from=build /src/out ./

EXPOSE 80
ENV ASPNETCORE_ENVIRONMENT Development
ENTRYPOINT ["dotnet", "AnotherSocialNetwork.Auth.dll"]
