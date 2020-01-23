FROM microsoft/aspnetcore:1.1.1
LABEL Name=NOC-PL-WebApplication Version=0.0.1
MAINTAINER Daniel Jackson
ARG source=.
WORKDIR /app
EXPOSE 80
COPY $source/published .
ENTRYPOINT dotnet NOC-PL-WebApplication.dll

#FROM microsoft/aspnetcore

#MAINTAINER Daniel Jackson

#WORKDIR /app
#COPY ./published .
#COPY ./published /app

#RUN ["dotnet", "start"]

#EXPOSE 5000

#ENTRYPOINT dotnet NOC-PL-WebApplication.dll
#ENTRYPOINT dotnet app/NOC-PL-WebApplication.dll

#FROM microsoft/aspnetcore:1.1
#LABEL Name=noc-pl-webapplication Version=0.0.1 
#ARG source=.
#WORKDIR /app
#EXPOSE 5000
#COPY NOC-PL-WebApplication/published ./
#ENTRYPOINT dotnet NOC-PL-WebAspplication.dll