FROM centos:latest

MAINTAINER sunlei333

# system update
RUN yum update -y

# basic tool
RUN yum install -y curl wget openssh bzip2 tar

# Development tools
RUN yum groupinstall -y "Development tools"


# fetch vim source
RUN yum install -y vim

# install Vundle
RUN git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim

# copy vimrc
RUN curl https://raw.githubusercontent.com/sunlei33/dev_config/master/.vimrc -o ~/.vimrc

#zsh
RUN yum install -y zsh

#set default zsh shell
RUN echo /usr/bin/zsh >> /etc/shells
RUN chsh -s /usr/bin/zsh

#tmux
RUN yum install -y ncurses-devel
RUN yum install -y libevent-devel
RUN wget https://raw.githubusercontent.com/sunlei33/docker-dev/master/tmux-2.3.tar.gz
RUN gunzip tmux-2.3.tar.gz
RUN tar xf tmux-2.3.tar
RUN cd tmux-2.3 && ./configure --prefix=/usr/local/tmux && make && make install && cd .. 
RUN ln -s /usr/local/tmux/bin/tmux /usr/local/bin/tmux


# copy tmux.conf
RUN curl https://raw.githubusercontent.com/sunlei33/dev_config/master/.tmux.conf -o ~/.tmux.conf

#nginx
RUN rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
RUN yum install -y nginx

#python
RUN yum install -y python-devel python3-devel
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py


#node
RUN wget https://raw.githubusercontent.com/sunlei33/docker-dev/master/node-v6.9.1-linux-x64.tar.xz
RUN xz -d node-v6.9.1-linux-x64.tar.xz
RUN tar xf node-v6.9.1-linux-x64.tar
RUN cp -r node-v6.9.1-linux-x64 /usr/local/node

RUN ln -s /usr/local/node/bin/node /usr/local/bin/node
RUN ln -s /usr/local/node/lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npm

RUN npm install -g eslint babel-eslint eslint-plugin-react webpack pm2 gulp typescript

# YCM
RUN yum install -y cmake
RUN git clone --recursive https://github.com/Valloric/YouCompleteMe.git ~/.vim/bundle/YouCompleteMe
RUN cd ~/.vim/bundle/YouCompleteMe && ./install.py --tern-completer && cd ~


#clean
RUN rm -f node-v6.9.1-linux-x64.tar tmux-2.3.tar npm-debug.log get-pip.py
RUN rm -rf tmux-2.3 node-v6.9.1-linux-x64

#oh-my-zsh
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# copy zshrc
RUN curl https://raw.githubusercontent.com/sunlei33/dev_config/master/.zshrc -o ~/.zshrc
