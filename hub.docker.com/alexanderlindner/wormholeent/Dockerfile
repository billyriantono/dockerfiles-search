FROM mysql:8.0

# install and setting locale
RUN apt-get update && \
    apt-get install -y locales && \
    rm -rf /var/lib/apt/lists/* && \
    echo "ja_JP.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen ja_JP.UTF-8
ENV LC_ALL ja_JP.UTF-8

# copy from custom my.cnf file
COPY ./my.cnf /etc/mysql/conf.d/
