FROM node:10.6.0-stretch

RUN apt-get update && \
    apt-get install -y apt-transport-https && \
    dpkg --add-architecture i386 && \
    bash -c "apt-key add <(curl https://dl.winehq.org/wine-builds/Release.key)" && \
    echo "deb https://dl.winehq.org/wine-builds/debian/ stretch main" > /etc/apt/sources.list.d/winehq.list && \
    apt-get update && \
    apt-get install -y winehq-stable
