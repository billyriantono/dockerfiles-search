FROM node

FROM jenkins/jenkins

USER root

COPY --from=0 /usr/local  /usr/local

RUN npm install -g @angular/cli

RUN apt-get update && \ 
    apt-get upgrade -y && \
    apt-get dist-upgrade -y

RUN apt-get install -y apt-transport-https \
    && apt-get install -y --no-install-recommends \
    curl libunwind8 gettext apt-transport-https && \
    curl https://packages.microsoft.com/keys/microsoft.asc |    gpg --dearmor > microsoft.gpg && \
    mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg && \
    sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" > /etc/apt/sources.list.d/dotnetdev.list' && \
    apt-get update

RUN apt-get install -y dotnet-sdk-2.2 && \
    export PATH=$PATH:$HOME/dotnet && \
    dotnet --version

RUN apt-get clean && apt-get autoremove -y

USER jenkins
