FROM ideploy/ubuntu:trusty-libuv-1.9.1
MAINTAINER WlniaoStudio <ideploy@wlniao.com>
ENV WLN_STARTUP_ROOT /wln
ENV WLN_LISTEN_PORT 5000
ENV DOTNET_VERSION 1.0.0-preview3-003215
EXPOSE 5000

RUN apt-get update \
    && apt-get install -y apt-transport-https libicu52 liblldb-3.6 liblttng-ust0 libunwind8 clang-3.5 \
    && echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list \
    && apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893 \
    && apt-get update
RUN apt-get install -y dotnet-dev-1.0.0-preview2-003121
	
	
WORKDIR /wln
ENTRYPOINT ["dotnet", "run"]
ONBUILD COPY . /wln
ONBUILD WORKDIR /wln
ONBUILD RUN dotnet restore
