ARG HOST_COMMIT=dev
ARG BUILD_NUMBER=00001
FROM microsoft/dotnet:2.2-sdk AS installer-env
ARG HOST_COMMIT
ARG BUILD_NUMBER

SHELL ["/bin/bash", "-c"]

ENV PublishWithAspNetCoreTargetManifest false

RUN export ARG_BUILD_NUMBER=${BUILD_NUMBER} && \
    if [[ $ARG_BUILD_NUMBER == dev* ]]; \
    then export SCRIPT_BUILD_NUMBER=00001; \
    else export SCRIPT_BUILD_NUMBER=$(echo $ARG_BUILD_NUMBER | cut -d'.' -f 3 | cut -d'-' -f 1); \
    fi && \
    echo "Build Number == $SCRIPT_BUILD_NUMBER" &&\
    wget https://github.com/Azure/azure-functions-host/archive/${HOST_COMMIT}.tar.gz && \
    tar xzf ${HOST_COMMIT}.tar.gz && \
    cd azure-functions-host-* && \
    dotnet publish -v q /p:BuildNumber="$SCRIPT_BUILD_NUMBER" /p:CommitHash=${HOST_COMMIT} src/WebJobs.Script.WebHost/WebJobs.Script.WebHost.csproj --output /azure-functions-host

# Runtime image
FROM microsoft/dotnet:2.2-aspnetcore-runtime
COPY --from=installer-env ["/azure-functions-host", "/azure-functions-host"]
COPY ./run-vaseks-afhost.sh /azure-functions-host/run-vaseks-afhost.sh

RUN sed -i 's/\r$//' /azure-functions-host/run-vaseks-afhost.sh  && \  
        chmod +x /azure-functions-host/run-vaseks-afhost.sh

WORKDIR /home/site/wwwroot

ENV AzureWebJobsScriptRoot=/home/site/wwwroot
ENV AzureFunctionsJobHost__Logging__Console__IsEnabled=true
ENV AzureWebJobsDashboard=""
ENV HOME=/home
ENV ASPNETCORE_URLS=http://+:80
EXPOSE 80

CMD /azure-functions-host/run-vaseks-afhost.sh
