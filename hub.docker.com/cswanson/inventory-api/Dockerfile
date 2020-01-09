FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Api.FoodBeverageInventory/Api.FoodBeverageInventory.csproj", "Api.FoodBeverageInventory/"]
COPY ["Domain.FoodBeverageInventory/Domain.FoodBeverageInventory.csproj", "Domain.FoodBeverageInventory/"]
COPY ["RavenDb.FoodBeverageInventory/RavenDb.FoodBeverageInventory.csproj", "RavenDb.FoodBeverageInventory/"]
RUN dotnet restore "Api.FoodBeverageInventory/Api.FoodBeverageInventory.csproj"
COPY . .
WORKDIR /src/Api.FoodBeverageInventory
RUN dotnet build "Api.FoodBeverageInventory.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Api.FoodBeverageInventory.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Api.FoodBeverageInventory.dll"]