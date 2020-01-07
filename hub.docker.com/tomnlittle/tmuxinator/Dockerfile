FROM ruby:alpine

RUN apk --update add \
    tmux \
    vim

RUN gem install tmuxinator

ENV EDITOR='vim'
ENV SHELL='ash'
