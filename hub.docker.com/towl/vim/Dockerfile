FROM towl/git

LABEL maintainer="Franck Coutouly <towl.fr@gmail.com>"

COPY docker-entrypoint /usr/local/bin/

RUN apk add --no-cache --update vim the_silver_searcher make bash && \
  mkdir -p ~/.vim/bundle /etc/.gist && \
  git clone https://github.com/Shougo/neobundle.vim ~/.vim/bundle/neobundle.vim && \
  git clone https://gist.github.com/bafa6dd7e5e81ba7cae69228cda83482.git /etc/.gist/vimrc && \
  rm /etc/vim/vimrc && \
  ln -s /etc/.gist/vimrc/.vimrc /etc/vim/vimrc && \
  chmod a+x /usr/local/bin/docker-entrypoint

ENV TERM=xterm-256color

ENTRYPOINT ["docker-entrypoint"]:
