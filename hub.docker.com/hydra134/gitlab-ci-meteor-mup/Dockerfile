FROM gitlab/gitlab-runner

LABEL maintainer="hydra134"

RUN apt-get update && \
    apt-get install -y npm sudo && \
    curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash - && \
    sudo apt-get install -y nodejs && \
    curl https://install.meteor.com/?release=1.6.1/ | sh && \
    npm install -g mup
