FROM ruby

RUN apt-get update && apt-get install -y vim zsh
COPY files/irbrc /root/.irbrc
COPY files/pre_vimrc /root/.vimrc
# Install Zsh 
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh \
  && cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc \
  && chsh -s /bin/zsh \
  && sed -ie 's/^  git/  git\n  ruby/g' /root/.zshrc

RUN git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
ENV  TERM='xterm-256color'
RUN vim +PluginInstall +qall
COPY files/vimrc /root/.vimrc