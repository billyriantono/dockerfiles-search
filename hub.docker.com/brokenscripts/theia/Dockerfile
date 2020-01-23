ARG NODE_VERSION=10.15.3
FROM node:${NODE_VERSION}-stretch

RUN apt-get update \
    && apt-get install -y \
         python \
         python-dev \
         python-pip \
         python3 \
         python3-dev \
         python3-pip \
         python3-venv \
    && apt-get clean \
    && rm -rf /var/cache/apt/* \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/*

RUN npm install -g yarn

RUN pip install \
      python-language-server \
      flake8 \
      pyflakes \
      autopep8 \
      pylint \
      pwntools \
      futures \
      configparser

RUN pip3 install \
      pylint \
      pyflakes \
      autopep8 \
      jupyter \
      nbconvert

WORKDIR /home/theia
ADD next.package.json ./package.json
ADD ms-python-release.vsix plugins/
ARG GITHUB_TOKEN
RUN yarn --cache-folder ./ycache && rm -rf ./ycache && \
    NODE_OPTIONS="--max_old_space_size=4096" yarn theia build
RUN mkdir /home/theia/project
EXPOSE 3000
ENV SHELL /bin/bash
CMD [ "yarn", "theia", "start", "--plugins=local-dir:./plugins", "--hostname=0.0.0.0", "/home/theia/project" ]
