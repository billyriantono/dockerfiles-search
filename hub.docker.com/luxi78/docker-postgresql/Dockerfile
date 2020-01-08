FROM postgres:9.6

RUN apt-get update && \
        apt-get upgrade -y && \
        apt-get install -y apt-utils && \
        apt-get install -y openssh-server tmux net-tools vim sudo && \
        apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
