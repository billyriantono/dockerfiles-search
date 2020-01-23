FROM microsoft/aspnetcore:latest
COPY . /blog
WORKDIR /blog

EXPOSE 5000/tcp
ENV ASPNETCORE_URLS http://*:5000
ENV ASPNETCORE_ENVIRONMENT docker

ENTRYPOINT ["dotnet", "Blog.dll"]