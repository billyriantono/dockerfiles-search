FROM node:6.9.0
ENV TERM xterm
RUN mkdir /www
WORKDIR /www

RUN apt-get update && apt-get -y install git-core zsh libnotify-bin
# Install Zsh
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh \
        && cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc \
        && chsh -s /bin/zshrc.zsh-template \ 
        && echo 'ZSH_THEME="remy"'  >> ~/.zshrc \
        && echo '[[ "$TERM" == "xterm" ]] && export TERM=xterm-256color' >> ~/.zshrc

RUN /bin/bash -c "cd /www && npm install -g notify-send gulp node-sass"
