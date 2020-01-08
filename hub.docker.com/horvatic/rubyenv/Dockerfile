FROM ubuntu:latest

ADD vimrc /

run apt update
run apt-get -y upgrade

run apt-get install -y ruby-full
run apt-get install -y vim
run apt-get install -y git

run git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
run mv vimrc ~/.vimrc
run vim -i NONE -c VundleUpdate -c quitall