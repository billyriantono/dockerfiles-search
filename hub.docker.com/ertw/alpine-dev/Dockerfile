FROM alpine:3.6
RUN apk update
RUN apk add vim curl git zsh wget openssh tree
WORKDIR /root/.vim/autoload/
ADD https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim plug.vim
WORKDIR /root
ADD https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh install.sh
RUN wget -O .vimrc https://raw.githubusercontent.com/ertw/dotfiles/master/init.vim
RUN vim +PlugInstall +qall 
RUN chmod +x install.sh
RUN ./install.sh ; exit 0
RUN rm .zshrc \
	&& mkdir /root/.ssh
RUN git clone https://github.com/ertw/dotfiles.git
RUN /root/dotfiles/create_dotfile_links.sh
ENV GIT_PAGER=more
