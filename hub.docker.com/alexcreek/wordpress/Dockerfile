FROM wordpress:5.2.3-php7.2
RUN apt update \
  && apt install less
RUN curl -o /usr/local/bin/wp https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
  && chmod +x /usr/local/bin/wp
RUN printf "alias wp='wp --allow-root'\n \
  alias ll='ls -l'" \
  > /root/.bashrc
