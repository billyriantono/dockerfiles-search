FROM microsoft/dotnet
WORKDIR /dotnetapp

# copy project.json and restore as distinct layers
COPY project.json .
RUN dotnet restore

# copy and build everything else
COPY . .
RUN dotnet publish -c Release -o out

# clean up build files
RUN rm -rf bin obj Dockerfile Program.cs

ENTRYPOINT ["dotnet", "out/dotnetapp.dll"]

