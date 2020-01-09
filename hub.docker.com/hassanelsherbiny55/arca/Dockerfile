#  run from comand 
#  docker run -d -P -v ~/grand/App_Data:/app/App_Data --name arcade  --network=host hassanelsherbiny55/arcade.template
# -v ~/grand/App_Data:/app/App_Data Maps The App_data Folder in container to the /grand/App_Data in Host
#  docker start arcade

 #this only install mongo but you need to run container ater that
 #  mkdir ~/data # create Directory for data on host machine
 # docker run -d -p 27017:27017 -v ~/data:/data/db mongo:3.4
 # Connect With Studio 3t Create User With All Roles then run mongo With Auth Mode
 # docker run -d -p 27017:27017  -v ~/data:/data/db  mongo:3.4 mongod --auth


#FROM mongo:3.4
FROM microsoft/dotnet:2.1-sdk AS build-env
WORKDIR /app
COPY ArcadeTemplate.sln .
COPY Grand.Core/Grand.Core.csproj Grand.Core/Grand.Core.csproj
COPY Grand.Data/Grand.Data.csproj Grand.Data/Grand.Data.csproj
COPY Grand.Framework/Grand.Framework.csproj Grand.Framework/Grand.Framework.csproj
COPY Grand.Services/Grand.Services.csproj Grand.Services/Grand.Services.csproj
COPY Grand.Web/Grand.Web.csproj Grand.Web/Grand.Web.csproj
#COPY Plugins/Grand.Plugin.ExternalAuth.Google/Grand.Plugin.ExternalAuth.Google.csproj Plugins/Grand.Plugin.ExternalAuth.Google/Grand.Plugin.ExternalAuth.Google.csproj
#COPY Plugins/Grand.Plugin.API/Grand.Plugin.API.csproj Plugins/Grand.Plugin.API/Grand.Plugin.API.csproj
#COPY Plugins/Grand.Plugin.ExternalAuth.Facebook/Grand.Plugin.ExternalAuth.Facebook.csproj Plugins/Grand.Plugin.ExternalAuth.Facebook/Grand.Plugin.ExternalAuth.Facebook.csproj
# Copy everything else and build
COPY . ./
RUN dotnet publish Grand.Web -c Release -o out
RUN dotnet build Plugins/Grand.Plugin.ExternalAuth.Facebook
RUN dotnet build Plugins/Grand.Plugin.ExternalAuth.Google
RUN dotnet build Plugins/Grand.Plugin.API
# Build runtime image
FROM microsoft/dotnet:2.1-aspnetcore-runtime 
RUN apt-get update &&  apt-get -y install libgdiplus
RUN ln -s /lib/x86_64-linux-gnu/libdl.so.2 /lib/x86_64-linux-gnu/libdl.so
WORKDIR /app
COPY --from=build-env /app/Grand.Web/out/ .
COPY --from=build-env /app/Grand.Web/Plugins/ ./Plugins/
VOLUME /app/App_Data /app/wwwroot /app/Plugins /app/Themes
ENTRYPOINT ["dotnet", "Grand.Web.dll"]
