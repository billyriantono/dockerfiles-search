FROM node:lts-stretch

# set apt mirror
COPY sources.list /etc/apt/sources.list

# install apt packages
RUN apt-get update && apt-get -y install sudo vim build-essential git python ruby tzdata zsh wget curl

# set timezone
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo Asia/Shanghai > /etc/timezone

# set up plain user(sudo,zsh)
RUN echo "node ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers && chsh -s $(which zsh)

# setup npm registry
ENV SASS_BINARY_SITE https://npm.taobao.org/mirrors/node-sass/
RUN npm i -g nrm --registry=https://registry.npm.taobao.org && nrm use taobao

# install global npm packages
RUN npm i -g pm2 trymodule lerna

# switch to user node
USER node
ENV SASS_BINARY_SITE https://npm.taobao.org/mirrors/node-sass/
RUN nrm use taobao

# oh my zsh
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
