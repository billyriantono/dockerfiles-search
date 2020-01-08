FROM mysql:8.0

RUN apt-get update && apt-get install -y mecab libmecab-dev mecab-ipadic-utf8 && \
    echo "loose-mecab-rc-file=/etc/mecabrc" >> /etc/mysql/conf.d/docker.cnf && \
    echo "innodb_ft_min_token_size=1" >> /etc/mysql/conf.d/docker.cnf

COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh
