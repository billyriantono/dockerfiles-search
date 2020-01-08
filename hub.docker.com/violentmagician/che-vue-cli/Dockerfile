FROM eclipse/stack-base:debian

RUN sudo apt-get update && \
    sudo apt-get -y upgrade && \
    sudo apt-get clean && \
    sudo apt-get -y autoremove && \
    sudo apt-get -y clean && \
    sudo rm -rf /var/lib/apt/lists/*

RUN wget -qO- https://deb.nodesource.com/setup_10.x | sudo -E bash -
RUN sudo apt update && sudo apt -y install nodejs

EXPOSE 8080
RUN sudo npm install --unsafe-perm -g yarn @vue/cli
