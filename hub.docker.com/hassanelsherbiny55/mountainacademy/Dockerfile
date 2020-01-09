#  run from comand 
# docker run -d -P -v ~/MountainAcademy/App_Data:/app/App_Data -v ~/MountainAcademy/Images:/app/wwwroot/Content/Images/  -v ~/MountainAcademy/LessonsFiles:/app/wwwroot/Content/LessonsFiles -v ~/MountainAcademy/Images1:/app/wwwroot/Content/Images1/ --name mountain  --network=host --restart always hassanelsherbiny55/mountainacademy
# -v ~/Mountain/App_Data:/app/App_Data Maps The App_data Folder in container to the /grand/App_Data in Host
#  docker start arcade

 #this only install mongo but you need to run container ater that
 #  mkdir ~/data # create Directory for data on host machine
 # docker run -d -p 27017:27017 -v ~/Mountain/MongoData:/data/db --name mongo mongo:3.4
 # Connect With Studio 3t Create User With All Roles then run mongo With Auth Mode
 # docker run -d -p 27017:27017  -v ~/Mountain/MongoData:/data/db  mongo:3.4 mongod --auth


#FROM mongo:3.4
FROM microsoft/dotnet:2.1-sdk AS build-env
WORKDIR /app
COPY MountainAcademy.sln .
COPY Grand.Core/Grand.Core.csproj Grand.Core/Grand.Core.csproj
COPY Grand.Data/Grand.Data.csproj Grand.Data/Grand.Data.csproj
COPY Grand.Framework/Grand.Framework.csproj Grand.Framework/Grand.Framework.csproj
COPY Grand.Services/Grand.Services.csproj Grand.Services/Grand.Services.csproj
COPY Grand.Web/Grand.Web.csproj Grand.Web/Grand.Web.csproj

# Copy everything else and build
COPY . ./
RUN dotnet publish Grand.Web -c Release -o out

# Build runtime image
FROM microsoft/dotnet:2.1-aspnetcore-runtime 
RUN apt-get update &&  apt-get -y install libgdiplus
RUN ln -s /lib/x86_64-linux-gnu/libdl.so.2 /lib/x86_64-linux-gnu/libdl.so
WORKDIR /app
COPY --from=build-env /app/Grand.Web/out/ .

VOLUME /app/App_Data /app/wwwroot /app/Plugins /app/Themes
ENTRYPOINT ["dotnet", "Grand.Web.dll"]
