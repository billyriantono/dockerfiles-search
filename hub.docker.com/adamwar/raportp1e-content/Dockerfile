FROM buildpack-deps:xenial-curl
MAINTAINER Adam May <adammay@gmail.com>

RUN locale-gen en_AU.UTF-8

ENV DEBIAN_FRONTEND noninteractive
ENV LANG en_AU.UTF-8
ENV LC_CTYPE en_AU.UTF-8
ENV LC_ALL en_AU.UTF-8
ENV HOME /home/developer

# Change default server and install dependencies
RUN sed -i "s/http:\/\/archive.ubuntu.com\/ubuntu\//http:\/\/mirror.internode.on.net\/pub\/ubuntu\/ubuntu\//g" /etc/apt/sources.list && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y \
            git \
            man \
            sudo \
            tmux \
            vim-nox \
            zsh && \
    rm -rf /var/lib/apt/lists/*

# Change the user that we're running as
RUN export uid=1000 gid=1000 && \
    mkdir -p /home/developer && \
    echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/zsh" >> /etc/passwd && \
    echo "developer:x:${uid}:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    chmod 0400 /etc/sudoers && \
    chown ${uid}:${gid} -R /home/developer

# Add custom .gitignore
RUN curl -o ${HOME}/.gitconfig https://raw.githubusercontent.com/adam-may/dotfiles/master/git/.gitconfig

# Setup zsh, including Oh-My-Zsh
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ${HOME}/.oh-my-zsh && \
    curl -o ${HOME}/.zshrc https://raw.githubusercontent.com/adam-may/dotfiles/master/zsh/.zshrc && \
    curl -o ${HOME}/.oh-my-zsh/themes/adammay.zsh-theme https://raw.githubusercontent.com/adam-may/dotfiles/master/zsh/adammay.zsh-theme

# Setup tmux
RUN curl -o ${HOME}/.tmux.conf https://raw.githubusercontent.com/adam-may/dotfiles/master/tmux/.tmux.conf

# Setup fonts
RUN git clone https://github.com/powerline/fonts.git ${HOME}/fonts && \
    ${HOME}/fonts/install.sh

# Setup vim.spf13/com
RUN curl -o ${HOME}/.vimrc.before.local https://raw.githubusercontent.com/adam-may/dotfiles/master/vim/.vimrc.before.local && \
    curl -o ${HOME}/.vimrc.bundles.local https://raw.githubusercontent.com/adam-may/dotfiles/master/vim/.vimrc.bundles.local && \
    curl -o ${HOME}/.vimrc.local https://raw.githubusercontent.com/adam-may/dotfiles/master/vim/.vimrc.local

# Setup spf13-vim
RUN curl http://j.mp/spf13-vim3 -L -o - | sh && \
    vim +BundleInstall +BundleClean +qall!

# Create the directory for our SSH keys
RUN mkdir ${HOME}/.ssh

USER developer
WORKDIR ${HOME}

CMD ["/bin/zsh"]

