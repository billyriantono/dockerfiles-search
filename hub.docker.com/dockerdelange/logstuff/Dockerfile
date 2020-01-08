#####################################################
#
#This Docker file Build the project in the subfolder,
#File belongs to: Cornel de Lange
#29 June 2018
#
##################################################
FROM microsoft/aspnetcore-build:2.0 AS build-env
#Copy everything in the project folders to app
COPY . /app
WORKDIR /app/LogStuff

RUN dotnet restore
#Test this Below works, but on wrong .db file
#RUN dotnet ef migrations add InitialCreate
#RUN dotnet ef database update
#Test end
RUN dotnet publish -c Release -o out

RUN mkdir /app/LogStuff/out/data

COPY UserIdentity.db /app/LogStuff/out/data

# Build runtime image
FROM microsoft/aspnetcore:2.0
WORKDIR /app/LogStuff
EXPOSE 80
COPY --from=build-env /app/LogStuff/out .
ENTRYPOINT ["dotnet", "LogStuff.dll"]
####################################################