FROM ubuntu:14.04

# INSTALL utilities
RUN apt-get update && \
    apt-get install -y ack-grep && \
    apt-get install -y curl && \
    apt-get install -y git && \
    apt-get install -y nodejs && \
    apt-get install -y npm && \
    apt-get install -y tree && \
    apt-get install -y vim && \
    apt-get install -y vim-nox && \
    apt-get install -y wget && \
    apt-get install -y xvfb && \
    apt-get install -y zsh && \
    # make link for node command & install oh-my-zsh
    ln -sf /usr/bin/nodejs /usr/bin/node && \
    wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

# INSTALL spf13
RUN curl https://j.mp/spf13-vim3 -L > spf13-vim.sh && \
    sh spf13-vim.sh && \
    # add custom settings for vim. includes: monokai colors & cursor settings
    curl -L https://bitbucket.org/api/1.0/repositories/willko/dot-files/raw/master/linux/.vimrc.local \
    >> /root/.vimrc.local

# INSTALL google-chrome
RUN wget -q -O - "https://dl-ssl.google.com/linux/linux_signing_key.pub" | sudo apt-key add - | echo 'deb http://dl.google.com/linux/chrome/deb/ stable main' >> /etc/apt/sources.list  && \
    apt-get update && apt-get install -y google-chrome-stable

# INSTALL protractor (for AngularJs testing)
RUN npm install -g protractor && \
    webdriver-manager update

# MOUNT this location for sharing with host
VOLUME /root/workspace

CMD zsh