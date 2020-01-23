##Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
##For more information, please see https://aka.ms/containercompat
#
#FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
#WORKDIR /app
#EXPOSE 80
#EXPOSE 443
#
#FROM microsoft/dotnet:2.1-aspnetcore-runtime AS build
#WORKDIR /src
##COPY ["SergelOnlineSPA/SergelOnlineSPA.csproj", "SergelOnlineSPA/"]
#RUN dotnet restore "SergelOnlineSPA/SergelOnlineSPA.csproj"
#COPY . .
#WORKDIR "/src/SergelOnlineSPA"
#RUN dotnet build "SergelOnlineSPA.csproj" -c Release -o /app
#
#FROM build AS publish
#RUN dotnet publish "SergelOnlineSPA.csproj" -c Release -o /app
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app .
#ENTRYPOINT ["dotnet", "SergelOnlineSPA.dll"]

FROM microsoft/dotnet:sdk AS build-env
WORKDIR /app

RUN apt-get update -yq && apt-get upgrade -yq && apt-get install -yq curl git nano
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && apt-get install -yq nodejs build-essential

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

#RUN dotnet publish "./SergelOnlineSPA.csproj" --output "./dist" --configuration Release --no-restore

# Build runtime image
FROM microsoft/dotnet:aspnetcore-runtime
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "SergelOnlineSPA.dll"]