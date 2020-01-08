# ======================================================================= 
# An image that contain basic stuff, i need in my dev tool chain:                          
# * zsh                                                              
# * git and tig                                                              
# * vim
# * node
# ======================================================================= 

FROM node:9.3.0-alpine
MAINTAINER samisdat bastian@pertz.eu

RUN apk update

# = some dependencies ===================================================================== 

RUN apk add htop
RUN apk add vim
RUN apk add wget
RUN apk add curl

# = git related stuff ===================================================================== 

RUN apk add git
RUN apk add tig

# set username and email
RUN git config --global user.name "samisdat"
RUN git config --global user.email bastian@pertz.eu

# use vim as git editor and open vim for commit messages in insert mode
RUN export VISUAL=vim
RUN export EDITOR="$VISUAL"
ADD vimrc /root/.vimrc

# == oh-my-zsh ==================================================================== 
RUN apk add zsh
ADD oh-my-zsh-install.sh /oh-my-zsh-install.sh
RUN chmod +x /oh-my-zsh-install.sh
RUN /oh-my-zsh-install.sh
RUN rm /oh-my-zsh-install.sh

WORKDIR /

EXPOSE 80

