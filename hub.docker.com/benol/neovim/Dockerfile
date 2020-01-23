FROM ubuntu:14.04

RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository -y ppa:rudenko/neovim \
  && apt-get update \
  && apt-get install -y neovim

CMD ["nvim"]
