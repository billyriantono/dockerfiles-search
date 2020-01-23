FROM mbrt/golang-vim-dev

ADD ./.bashrc /home/dev/.bashrc
ADD ./.vimrc /home/dev/.vimrc

RUN vim +PluginInstall +qall
