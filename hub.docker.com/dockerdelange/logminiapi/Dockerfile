#####################################################
#
#File belongs to: Cornel de Lange
#4 August 2018
#Image name dockerdelange/logminiapi
#################################################
FROM microsoft/aspnetcore-build:2.0 AS build-env
#Copy everything in the twin project folders to app
#not sure yet why I have to use a folder called app
COPY . /app
WORKDIR /app/LogMiniAPI

RUN dotnet restore
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/aspnetcore:2.0
WORKDIR /app/LogMiniAPI
EXPOSE 80
COPY --from=build-env /app/LogMiniAPI/out .
ENTRYPOINT ["dotnet", "LogMiniAPI.dll"]
####################################################