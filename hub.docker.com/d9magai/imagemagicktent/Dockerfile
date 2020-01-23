FROM centos:7
RUN curl -O https://nodejs.org/dist/v10.9.0/node-v10.9.0-linux-x64.tar.xz
RUN tar xvf node-v10.9.0-linux-x64.tar.xz
ENV PATH /node-v10.9.0-linux-x64/bin:$PATH
RUN echo 'alias cnpm="npm --registry=https://registry.npm.taobao.org \
  --cache=$HOME/.npm/.cache/cnpm \
  --disturl=https://npm.taobao.org/dist \
  --userconfig=$HOME/.cnpmrc"' > ~/.zshrc && source ~/.zshrc
RUN npm install -g yarn
