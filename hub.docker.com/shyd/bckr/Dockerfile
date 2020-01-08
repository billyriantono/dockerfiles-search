FROM shyd/zsh

RUN apt-get update && \
    apt-get -y install mysql-client encfs sshfs

RUN rm -rf /var/lib/apt/lists/*
