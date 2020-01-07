FROM ubuntu:18.04

RUN apt update 
RUN apt install git vim sudo curl tree -y
RUN apt install htop -y
RUN apt install man -y

# create another demo user
RUN adduser --quiet --disabled-password --gecos "User" person1 && adduser person1 sudo
RUN echo "person1:password1" | chpasswd

# install zsh and oh-my-zsh
RUN apt install zsh -y
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# set default command if no command is passed when starting container
CMD [ "zsh" ]

# clone personal dotfiles
RUN git clone https://github.com/frankfuu/dotfiles.git ~/dotfiles
RUN cd ~/dotfiles/ubuntu && chmod +x install.sh
RUN ~/dotfiles/ubuntu/install.sh
RUN mkdir -p ~/.ssh

# install plugins
RUN git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
RUN ~/.fzf/install