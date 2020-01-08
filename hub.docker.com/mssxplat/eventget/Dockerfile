
# we use ARGS here because they can be overriden for 'docker build' 

FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk as dotnet-build
WORKDIR /src

FROM dotnet-build as publish
WORKDIR /src
COPY . .

ARG BUILD_VERBOSITY=quiet
ARG BUILD_CONFIGURATION=Release
ARG BUILD_NUMBER=0000
RUN chmod +x ./cli-linux/build-inside-docker.sh
RUN ./cli-linux/build-inside-docker.sh $BUILD_VERBOSITY $BUILD_CONFIGURATION

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "EventGet.Web.dll"]
