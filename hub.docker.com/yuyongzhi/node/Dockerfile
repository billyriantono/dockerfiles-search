#基于 centos7 构建 node 环境
FROM yuyongzhi/centos7:latest as source

SHELL ["/bin/bash", "-c"]

RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.0/install.sh | bash

RUN echo '' >> /etc/profile \
  && echo 'export NVM_DIR=$HOME/.nvm' >> /etc/profile \
  && echo 'source $NVM_DIR/nvm.sh' >> /etc/profile \
  && echo 'source $NVM_DIR/bash_completion' >> /etc/profile \
  && echo '' >> /etc/profile \
  && source /etc/profile \
  && nvm install 11.11.0
