FROM alpine

MAINTAINER Romain Commandé, commande.romain@gmail.com

RUN adduser devbox -h /devbox user -D

RUN apk add --no-cache zsh curl git python3
RUN pip3 install powerline-status

USER devbox
WORKDIR /devbox
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" || true
#RUN rm /devbox/.zshrc
ADD files/zshrc /devbox/.zshrc

#RUN git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
#RUN git clone https://github.com/jeremyFreeAgent/oh-my-zsh-powerline-theme.git ~/.oh-my-zsh/custom/themes/powerline
RUN git clone https://github.com/zsh-users/zsh-autosuggestions.git ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions


#USER root
ENV TERM xterm-256color


ENTRYPOINT zsh
