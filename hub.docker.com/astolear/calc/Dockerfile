############# STAGE 1 - Angular build ###############
FROM astolear/angular-cli:1.5.0 as angular-builder

WORKDIR /app

# copy package.json and install packages as distinct layers
COPY package.json package-lock.json ./
RUN npm set progress=false && npm install

# copy everything else and build
COPY . ./
RUN ng build --prod --progress=false

############# STAGE 2 - Dotnet build ###############
FROM microsoft/aspnetcore-build:2.0.2 as dotnet-builder

WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out --no-restore

############# STAGE 3 - Merge ###############
FROM microsoft/aspnetcore:2.0
LABEL authors="Artur Stolear <artur.stolear@gmail.com>"

WORKDIR /app

# copy from builder containers
COPY --from=dotnet-builder  /app/out ./
COPY --from=angular-builder /app/wwwroot ./wwwroot

ENTRYPOINT ["dotnet", "client.dll"]
