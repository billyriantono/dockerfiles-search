FROM microsoft/dotnet:1.0.4-sdk
MAINTAINER Frank Pommerening "frank@pommerening-online.de"
ENV REFRESHED_AT 2017-03-10

COPY WebApp/ /WebApp

RUN cd /WebApp && dotnet restore && dotnet build
WORKDIR /WebApp
EXPOSE 8080
ENTRYPOINT ["dotnet", "run"]
