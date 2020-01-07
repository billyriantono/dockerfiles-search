FROM node:latest
RUN apt-get update
RUN apt-get -y dist-upgrade
RUN apt-get install -y vim zsh vlc rtmpdump git monit
RUN sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" || true
RUN echo "alias sb='source ~/.zshrc'" >> ~/.zshrc
RUN echo "alias vbp='vim ~/.zshrc'" >> ~/.zshrc
RUN echo "cd" >> ~/.zshrc
RUN mkdir -p ~/.vim/autoload ~/.vim/bundle && curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim
RUN echo "execute pathogen#infect()\nsyntax on\nfiletype plugin indent on\n" >> ~/.vimrc
RUN echo "set wildmenu\nset wildmode=list:longest" >> ~/.vimrc
RUN apt-get install -y man less
RUN cd ~/.vim/bundle
RUN git clone git://github.com/altercation/vim-colors-solarized.git
RUN echo "syntax enable\nset background=dark\ncolorscheme solarized\n" >> ~/.vimrc
RUN apt-get install -y screen
