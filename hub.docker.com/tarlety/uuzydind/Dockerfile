FROM ubuntu:latest
LABEL maintainer="tarlety@gmail.com"

RUN apt-get update \
 && apt-get upgrade -y \
 && apt-get install -y wget curl zsh git vim make sudo dmsetup \
 && apt-get install -y tmux lynx \
 && apt-get clean \
 && rm -r /var/lib/apt/lists/*

# dind, https://github.com/jpetazzo/dind
RUN curl -sSL https://get.docker.com/ | sh
ADD https://raw.githubusercontent.com/jpetazzo/dind/master/wrapdocker /usr/local/bin/wrapdocker
RUN chmod +x /usr/local/bin/wrapdocker
VOLUME /var/lib/docker

# docker-compose
RUN sudo curl -L https://github.com/docker/compose/releases/download/1.19.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose

# default user, me
RUN useradd -ms /bin/zsh me
RUN usermod -aG docker me
RUN usermod -aG sudo me
RUN echo "me ALL=(ALL:ALL) NOPASSWD: ALL" > /etc/sudoers.d/me
USER me

# oh-my-zsh, https://github.com/robbyrussell/oh-my-zsh
RUN sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"; exit 0
RUN git clone git://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/plugins/zsh-autosuggestions

# zsh's theme and plugins
RUN sed -i -e 's/ZSH_THEME="robbyrussell"/ZSH_THEME="ys"/g' ~/.zshrc
RUN sed -i -e 's/plugins=(/plugins=( zsh-autosuggestions/g' ~/.zshrc
RUN sed -i -e "s/ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=8'/ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=red'/g" ~/.oh-my-zsh/plugins/zsh-autosuggestions/src/config.zsh
RUN cd ~/.oh-my-zsh/plugins/zsh-autosuggestions/ ; make

# initial dind, and start user's shell
USER root
CMD ["bash", "-c", "/usr/local/bin/wrapdocker su - me"]
