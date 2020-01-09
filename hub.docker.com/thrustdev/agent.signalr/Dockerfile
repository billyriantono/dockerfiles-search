FROM microsoft/dotnet:2.1-sdk-alpine AS build-env
WORKDIR /app

# copy and build everything else
COPY . ./

# Change work directory
WORKDIR Thrust.SCooB.Agents.SignalR

# Install app dependencies
#RUN npm install

# Package to output directory
RUN dotnet publish -c Release -o out Thrust.SCooB.Agents.SignalR.csproj

# Build da imagem
FROM microsoft/dotnet:2.1-aspnetcore-runtime
WORKDIR /app

# Binds to ports
EXPOSE  7000

COPY --from=build-env /app/Thrust.SCooB.Agents.SignalR/out .
ENTRYPOINT ["dotnet", "Thrust.SCooB.Agents.SignalR.dll"]