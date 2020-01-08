FROM ubuntu:latest

ADD vimrc /

run apt update
run apt-get -y upgrade
run apt-get install -y ca-certificates
run apt-get install -y apt-transport-https
run apt-get install -y software-properties-common

run apt-get install -y wget
run apt-get install -y vim
run apt-get install -y git

run wget -q https://packages.microsoft.com/config/ubuntu/19.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
run dpkg -i packages-microsoft-prod.deb
run apt-get -y update
run apt-get -y install dotnet-sdk-2.2

run git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
run mv vimrc ~/.vimrc
run vim -i NONE -c VundleUpdate -c quitall