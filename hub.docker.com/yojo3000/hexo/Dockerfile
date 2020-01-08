From ubuntu:latest

RUN apt update; apt upgrade -y; apt autoremove -y;
RUN apt update --fix-missing;

RUN apt install \
vim \
git \
curl \
-y

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash

RUN echo 'export NVM_DIR="$HOME/.nvm"' > /root/.bashrc
RUN echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"' >> /root/.bashrc
RUN echo '[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"' >> /root/.bashrc

# 為啥 source 之後再做 RUN 就看不懂 .bashrc 了，一定要寫在一行是怎樣？
RUN /bin/bash -c 'source /root/.bashrc; \
nvm install stable; \
npm install -g hexo-cli; '

RUN mkdir /hexo_blog
