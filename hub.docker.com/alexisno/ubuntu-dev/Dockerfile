# Use ubuntu:latest as base image.
FROM ubuntu:latest

MAINTAINER Alexis N-o "alexis@henaut.net"

# Install basic packages.
RUN apt-get update &&\
    apt-get install -y software-properties-common zsh curl wget git htop unzip vim telnet &&\
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Install oh-my-zsh and define zsh as default shell
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true &&\
    chsh -s /bin/zsh

# Apply custom theme, disable auto-update and fix backspace displaying space in the prompt
COPY /root/.oh-my-zsh/themes/anoio-docker.zsh-theme /root/.oh-my-zsh/themes/anoio-docker.zsh-theme
RUN sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="anoio-docker"/g' /root/.zshrc &&\
    sed -i 's/# DISABLE_AUTO_UPDATE=true/DISABLE_AUTO_UPDATE=true/g' /root/.zshrc &&\
    echo TERM=xterm >> /root/.zshrc

# Apply custom .gitconfig
COPY /root/.gitconfig /root/.gitconfig

# Create dev user
RUN useradd dev -m -d /home/dev/ -s /bin/zsh -G sudo && passwd -d -u dev

# Add a script to modify the dev user UID / GID
COPY /usr/local/bin/change-dev-id /usr/local/bin/change-dev-id
RUN chmod +x /usr/local/bin/change-dev-id

# Configure zsh and git for user dev
USER dev
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true &&\
    sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="anoio-docker"/g' /home/dev/.zshrc &&\
    sed -i 's/# DISABLE_AUTO_UPDATE=true/DISABLE_AUTO_UPDATE=true/g' /home/dev/.zshrc &&\
    echo TERM=xterm >> /home/dev/.zshrc
COPY /home/dev/.oh-my-zsh/themes/anoio-docker.zsh-theme /home/dev/.oh-my-zsh/themes/anoio-docker.zsh-theme
USER root
RUN cp /root/.gitconfig /home/dev/.gitconfig && chown dev:dev /home/dev/.gitconfig

CMD ["/bin/zsh"]
