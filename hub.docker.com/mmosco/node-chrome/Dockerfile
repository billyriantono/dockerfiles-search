FROM node:lts

USER root

RUN apt-get update \
      && apt-get upgrade -y \
      && apt-get install -y libxss1 libappindicator1 libindicator7 \
    && wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    && apt install -y ./google-chrome*.deb \
    && rm -rf /var/lib/apt/lists/* ./google-chrome*.deb

USER node

