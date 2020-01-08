FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src

# copy csproj and restore as distinct layers
#COPY ./VinoValtech.Supreme.sln .
#COPY ./src/API/Vino.API.csproj ./src/API/Vino.API.csproj
#COPY ./src/Models/Vino.Models.csproj ./src/Models/Vino.Models.csproj
#COPY ./src/Test/Vino.Test.csproj ./src/Test/Vino.Test.csproj
COPY . .
RUN dotnet publish VinoValtech.Supreme.sln -c Release -o out

FROM microsoft/dotnet:2.2-aspnetcore-runtime AS runtime
WORKDIR /app
COPY --from=build /src/src/API/out ./
ENTRYPOINT ["dotnet", "Vino.API.dll"]