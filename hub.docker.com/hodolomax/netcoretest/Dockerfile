FROM mcr.microsoft.com/dotnet/core/aspnet:2.1
WORKDIR /app
#LABEL io.k8s.display-name="app" \
#      io.k8s.description="container description..." \
#      io.openshift.expose-services="8080:http"
COPY WebApplication1/out/ .
EXPOSE 8080
ENV ASPNETCORE_URLS=http://*:8080
ENTRYPOINT [ "dotnet","WebApplication1.dll" ]
