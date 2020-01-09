#FROM microsoft/aspnet:1.0.0-beta8-coreclr
FROM microsoft/aspnet:1.0.0-rc1-update1-coreclr
 
ADD . /project
 
WORKDIR /project
 
RUN ["dnu", "restore"]
 
ENTRYPOINT ["dnx", "web", "--server.urls", "http://0.0.0.0:5000"]
