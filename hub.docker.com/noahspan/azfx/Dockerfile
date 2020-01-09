FROM ubuntu:18.10

RUN apt-get update && \
    apt-get -y install sudo && \
    apt-get -y install curl && \
    apt-get -y install lsb-release && \
    apt-get -y install gnupg && \
    curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg && \
    mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg && \
    sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-$(lsb_release -cs)-prod $(lsb_release -cs) main" > /etc/apt/sources.list.d/dotnetdev.list' && \
    mkdir -p /usr/app/azfx

RUN apt-get update && \
    apt-get -y install azure-functions-core-tools

RUN apt-get update && \
    apt-get -y install nodejs && \
    apt-get -y install npm

VOLUME /usr/app/azfx
WORKDIR /usr/app/azfx

RUN useradd --create-home --shell /bin/bash azfx && \
    usermod -aG sudo azfx && \
    chown -R azfx:azfx /usr/app/azfx

USER azfx

CMD /bin/bash