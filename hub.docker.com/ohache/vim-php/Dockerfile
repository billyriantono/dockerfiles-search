FROM alpine:latest

COPY vimrc /root/.vimrc
COPY coc-settings.json /root/.vim/coc-settings.json

RUN apk update && \
	# 安装相关工具
	apk add --no-cache git vim tmux python3 curl zsh php7 composer nodejs yarn npm ctags php7-tokenizer

	# php 补全命令
RUN	npm i intelephense -g && \
	# 安装oh-my-zsh
	sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)" && \
	# 安装vim-plug
	curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim && \
	# 添加php-cs-fixer
	composer global require friendsofphp/php-cs-fixer && \
	echo 'export PATH=$PATH:/root/.composer/vendor/bin' >> /root/.zshrc
