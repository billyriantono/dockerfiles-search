FROM golang:1.7.1

RUN apt-get update && apt-get --assume-yes install vim-gtk git curl

COPY ./vimrc /root/.vimrc

RUN curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

RUN vim -c "PlugInstall" -c "qa"

RUN vim -c "GoInstallBinaries" -c "qa" 
