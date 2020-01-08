FROM gitpod/workspace-postgres

# add your tools here
USER root

# Install custom tools, runtime, etc.
RUN wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | sudo apt-key add - && \
      sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
RUN add-apt-repository ppa:lazygit-team/release
RUN add-apt-repository ppa:neovim-ppa/stable
RUN apt-get update && apt-get install -y \
        google-chrome-stable \
        lazygit \
        neovim \
        silversearcher-ag \
        tmux \
        vim \
        zsh \
    && apt-get clean && rm -rf /var/cache/apt/* && rm -rf /var/lib/apt/lists/* && rm -rf /tmp/*

USER gitpod
# Apply user-specific settings

ENV TERM="xterm-256color"
# install custom dev env
RUN cd $HOME && git clone https://github.com/deepflame/dotfiles.git && cd dotfiles && ./install.sh && vim +PlugInstall +qall > /dev/null

# Give back control
USER root
