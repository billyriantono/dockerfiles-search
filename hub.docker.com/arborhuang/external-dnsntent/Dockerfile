FROM kkarczmarczyk/node-yarn
ENV TERM xterm
RUN mkdir /www
WORKDIR /www
# Install Zsh
RUN apt-get update && apt-get -y install apt-utils git-core zsh libnotify-bin
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh \
        && cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc \
        && echo 'ZSH_THEME="remy"'  >> ~/.zshrc \
        && echo '[[ "$TERM" == "xterm" ]] && export TERM=xterm-256color' >> ~/.zshrc

RUN /bin/bash -c "cd /www && npm install -g notify-send gulp node-sass"
RUN npm rebuild node-sass 
RUN npm rebuild node-gyp
