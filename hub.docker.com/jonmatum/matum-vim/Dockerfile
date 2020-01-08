FROM jonmatum/matum-shell:latest

MAINTAINER Jonatan Mata

RUN apt-get update && apt-get install -y vim

RUN bash -c "$(curl -H 'Cache-Control: no-cache' -fsSL https://raw.githubusercontent.com/jonmatum/dotfiles/master/setup/vim.bash)"

CMD vim
