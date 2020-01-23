FROM mono:5.2

RUN apt-get update
RUN apt-get install apt-transport-https -y

RUN bash -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ wheezy main" > /etc/apt/sources.list.d/azure-cli.list'
RUN apt-key adv --keyserver packages.microsoft.com --recv-keys 417A0893

RUN apt-get update
RUN apt-get install git-core azure-cli zip unzip -y

RUN apt-get clean
RUN rm -rf /var/cache/apt/*

RUN nuget update -self
