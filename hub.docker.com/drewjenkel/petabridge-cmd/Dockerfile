FROM microsoft/dotnet:sdk AS build-env
WORKDIR /app
# We are installing this in a separate container with the SDK
RUN dotnet tool install --global pbm
FROM microsoft/dotnet:aspnetcore-runtime AS runtime
WORKDIR /app
# We are copying into a runtime image so we have a smaller image to download.
COPY --from=build-env /root/.dotnet /root/.dotnet
# Needed because https://stackoverflow.com/questions/51977474/install-dotnet-core-tool-dockerfile
ENV PATH="${PATH}:/root/.dotnet/tools"