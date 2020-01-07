FROM ubuntu

RUN sudo apt-get update; \
    sudo apt-get install -y curl; \
    curl -sL https://deb.nodesource.com/setup_0.12 | sudo bash -; \
    sudo apt-get update; \
    sudo apt-get install -y firefox nodejs Xvfb

ADD entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
