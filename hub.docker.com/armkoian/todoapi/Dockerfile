FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
# COPY .src/*.sln .
COPY src/ ./
RUN dotnet restore

# copy everything else and build app
# COPY aspnetapp/. ./aspnetapp/
# WORKDIR /app/aspnetapp
RUN dotnet publish -c Release -o out


FROM mcr.microsoft.com/dotnet/core/aspnet:3.0 AS runtime

WORKDIR /app
COPY --from=build /app/out ./
ENV ASPNETCORE_URLS="http://*:80"
# ENTRYPOINT ["dotnet", "src.dll"]
# ENTRYPOINT ["dotnet", "src.dll"]
# ENTRYPOINT ["/bin/sh]
CMD [ "./src" ]
EXPOSE 80
