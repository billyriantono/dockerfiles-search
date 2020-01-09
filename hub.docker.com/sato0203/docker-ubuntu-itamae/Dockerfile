#base OS
FROM ubuntu:16.04

# setup
RUN apt update -y && \
    apt upgrade -y && \
    apt install -y rbenv ruby-build ruby-dev sudo && \
    echo 'eval "$(rbenv init -)"' >> $HOME/.bashrc && \
    . $HOME/.bashrc && \
    hash -r && \
    rbenv install 2.2.3 && \
    rbenv global 2.2.3 && \
    gem install itamae