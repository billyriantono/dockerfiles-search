FROM docker:stable

ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8

RUN apk add --no-cache \
	ca-certificates \
	curl \
	git \
 	bash \
	vim \
	tmux \
	openssh \
	openssh-client \
	zsh \
	ansible

RUN mkdir -p .vim/bundle/ \
	&& git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim

COPY .bash_profile /root/
COPY .zshrc /root/
COPY .tmux.conf /root/
COPY .gitconfig /root/.gitconfig
COPY .vimrc /root/.vimrc

RUN vim +silent +PluginInstall +qall

# RUN ssh-keygen -b 4096 -t rsa -q -N "" -C "ansiblemaster" -f /root/.ssh/id_rsa

WORKDIR /data

ENTRYPOINT ["/bin/zsh"]
