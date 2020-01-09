FROM debian

MAINTAINER Morten Olsen <morten@olsen.io>

ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8' TERM='xterm-256color'

RUN apt-get update \
    && apt-get install -y git zsh tmux wget gpg vim python3-pip

RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

RUN echo 'deb http://http.kali.org/kali kali-rolling main contrib non-free' >> /etc/apt/sources.list
RUN gpg --keyserver pgpkeys.mit.edu --recv-key  ED444FF07D8D0BF6 \
    && gpg -a --export ED444FF07D8D0BF6 | apt-key add -

RUN apt-get update \
    && apt-get install -y hydra john dirb wordlists nmap \
       medusa metasploit-framework ruby recon-ng

RUN pip3 install jupyter scipy panda

COPY ./scripts /scripts
COPY ./wordlists /wordlists

VOLUME /workspace
WORKDIR /workspace

RUN chsh -s /bin/zsh

CMD ["zsh"]
