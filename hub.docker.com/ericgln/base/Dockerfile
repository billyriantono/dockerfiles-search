FROM ubuntu:latest

# Installing goodies
RUN apt-get update -y
RUN apt-get install man software-properties-common git zsh wget curl -y

# Installing development tools
RUN apt-get install build-essential python python3 python-dev python3-dev -y

# Installing Neovim
RUN add-apt-repository ppa:neovim-ppa/stable -y
RUN apt-get update -y
RUN apt-get install neovim -y

# Configuring Neovim
ENV EDITOR=nvim
RUN curl https://raw.githubusercontent.com/dotpy3/dotfiles/master/.vimrc -o /root/.vimrc

# Setting shell
ENTRYPOINT /usr/bin/zsh
