FROM microsoft/dotnet:2.2-sdk-alpine
RUN apk add --update nodejs nodejs-npm openjdk8-jre nss

ENV PATH="${PATH}:/root/.dotnet/tools"
ENV CI_PROJECT_NAME=$CI_PROJECT_NAME
ENV CI_SONAR=$CI_SONAR
ENV CI_LOGIN=$CI_LOGIN

RUN dotnet tool install --global dotnet-sonarscanner
