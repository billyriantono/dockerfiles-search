#standard ubuntu for me
FROM ubuntu:14.04
MAINTAINER tujed1 <studentofgraz@gmail.com>
RUN apt-get -yq update && apt-get install -yq zsh wget
RUN wget -q -O /etc/zsh/zshrc http://git.grml.org/f/grml-etc-core/etc/zsh/zshrc
RUN apt-get clean && rm -rf /var/lib/apt/lists/*
RUN chsh -s /usr/bin/zsh
