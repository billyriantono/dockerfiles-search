FROM microsoft/dotnet:2.2-runtime

# Map port 80
EXPOSE 80/tcp

# You have to set this variable to your webapi dll
ENV RUN_DLL="MyApp.dll"

# Map this folder to your bin folder
WORKDIR /app

# Run our application
ENTRYPOINT ["sh", "-c", "dotnet $RUN_DLL"]
