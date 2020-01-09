#####################################################
#
#This Docker file lets two projects(dependency) build,
#due to dotnet core *.csproj dependency on the repo project
#File belongs to: Cornel de Lange
#4 July 2018
#Image name dockerdelange/logtapi
#################################################
FROM microsoft/aspnetcore-build:2.0 AS build-env
#Copy everything in the twin project folders to app
#not sure yet why I have to use a folder called app
COPY . /app
WORKDIR /app/LogAPI
#The 2 project are connected in the LogAPI.csproj file
#LogAPI declares the dependency there for FaultsRepo
#Dotnet Core does its build magic from there from FaultsAPI.dll
RUN dotnet restore
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/aspnetcore:2.0
WORKDIR /app/LogAPI
EXPOSE 80
COPY --from=build-env /app/LogAPI/out .
ENTRYPOINT ["dotnet", "LogAPI.dll"]
####################################################