FROM microsoft/dotnet:latest
COPY . /web
WORKDIR /web
 
RUN ["dotnet", "restore"]
RUN ["dotnet", "build"]
 
EXPOSE 5000/tcp
ENV ASPNETCORE_URLS http://*:5000/
 
ENTRYPOINT ["dotnet", "run"]