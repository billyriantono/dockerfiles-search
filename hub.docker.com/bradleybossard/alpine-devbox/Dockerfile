FROM alpine
MAINTAINER Bradley Bossard <bradleybossard@gmail.com>

RUN apk update && apk upgrade

#RUN apk remove ack

RUN apk add git \
            tig \
            curl \
            wget \
            tmux \
            vim \
            bash \
            perl \
            ack \
            tree

WORKDIR /root
RUN git clone https://github.com/bradleybossard/dotfiles.git
RUN git clone https://github.com/gmarik/vundle.git ./.vim/bundle/vundle
RUN cd dotfiles; sh setup.sh;

ENV TERM xterm

ENTRYPOINT [ "bash" ]

