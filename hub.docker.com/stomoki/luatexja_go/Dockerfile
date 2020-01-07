FROM ubuntu:16.04
MAINTAINER Tomoki Sugiura

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y curl wget git language-pack-ja-base language-pack-ja && apt-get clean -y
RUN update-locale LANG=ja_JP.UTF-8 LANGUAGE="ja_JP:ja"
# RUN apt-add-repository ppa:texlive-backports/ppa
RUN apt-get install texlive-lang-japanese texlive-science texlive-extra-utils texlive-luatex texlive-latex-extra texlive-latex-recommended texlive-fonts-extra -y && apt-get clean -y
RUN apt-get install golang-go -y && apt-get clean -y && go version
# golang settings
ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH
RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
