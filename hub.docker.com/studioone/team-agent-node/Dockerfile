FROM jetbrains/teamcity-agent
LABEL maintainer="Asdrubal Gonzalez" \
    description="This image for testing"
RUN apt update \
    && apt upgrade -y \
    && apt install apt-utils -y \
    && apt install -y --no-install-recommends build-essential
RUN curl -sL https://deb.nodesource.com/setup_10.x -o /root/nodesource_setup.sh \
    && bash /root/nodesource_setup.sh \
    && apt install nodejs -y \
    && npm install typescript -g \
    && apt install rsync -y \
    && apt autoremove \
    && rm -rf /var/lib/apt/lists/*
