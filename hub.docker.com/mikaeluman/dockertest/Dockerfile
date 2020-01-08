FROM fsharp:netcore

ADD . proj/
RUN cd proj && chmod +x ./fake.sh && ./fake.sh build
ENTRYPOINT ["dotnet", "run", "--project", "proj/src/DockerFs"]