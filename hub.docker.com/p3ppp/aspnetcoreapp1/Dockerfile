FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.sln .
COPY aspnetcoreapp1/*.csproj ./aspnetcoreapp1/
RUN dotnet restore

# copy everything else and build app
COPY aspnetcoreapp1/. ./aspnetcoreapp1/
WORKDIR /app/aspnetcoreapp1
RUN dotnet publish -c Release -o out


FROM microsoft/dotnet:2.1-aspnetcore-runtime AS runtime
WORKDIR /app
COPY --from=build /app/aspnetcoreapp1/out ./
RUN ls
ENTRYPOINT ["dotnet", "aspnetcoreapp1.dll"]