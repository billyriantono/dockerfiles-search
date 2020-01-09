FROM microsoft/aspnet:1.0.0-rc1-update1
COPY ./src/RESTApp/project.json /app/
WORKDIR /app
RUN ["dnu", "restore"]
COPY ./src/RESTApp/. /app
EXPOSE 5000
ENV SERVER.URLS http://*:5000
ENTRYPOINT ["dnx", "-p", "project.json", "web"]
