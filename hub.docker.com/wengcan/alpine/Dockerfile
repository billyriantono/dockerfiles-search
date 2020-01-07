FROM alpine:3.7

MAINTAINER wengcan <wengcanvip@gmail.com>

RUN apk add --update --no-cache bash tar byobu zsh  shadow curl git unzip vim wget python python-dev py-pip py-virtualenv openssh-client  util-linux\
  && pip install virtualenv \
  && rm -rf /var/cache/apk/*

# Add files.
ADD root/.bashrc /root/.bashrc
ADD root/.gitconfig /root/.gitconfig
ADD root/.scripts /root/.scripts

RUN git clone git://github.com/bwithem/oh-my-zsh.git /root/.oh-my-zsh \
    && cp /root/.oh-my-zsh/templates/zshrc.zsh-template /root/.zshrc \
    && chsh -s /bin/zsh

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

# Define default command.
CMD ["zsh"]
