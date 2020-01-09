FROM microsoft/dotnet:latest

WORKDIR /root
# Copy the app file to root

COPY ./ /root

# Configure the listening port to 9100
EXPOSE 9100/tcp

# Start the app
ENTRYPOINT dotnet firstwebapi.dll
