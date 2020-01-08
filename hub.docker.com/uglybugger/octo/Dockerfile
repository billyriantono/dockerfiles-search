FROM microsoft/dotnet:2.1-runtime

WORKDIR /octo
RUN curl https://download.octopusdeploy.com/octopus-tools/4.37.0/OctopusTools.4.37.0.portable.tar.gz | tar zxv

ENTRYPOINT ["dotnet","Octo.dll"]

