FROM python:2.7

MAINTAINER Dominik Ruf <dominikruf@gmail.com>

ENV DEBIAN_FRONTEND=noninteractive
ENV KALLITHEA_PATH /var/kallithea

RUN apt-get update && \
    apt-get install -y \
        python-dev \
        python-ldap \
        pwgen && \
    pip install --upgrade pip \
        setuptools \
        mercurial \
        psycopg2 \
        mysql-python && \
    useradd -d /var/kallithea -u 1000 -m -s /bin/bash kallithea && \
    apt-get purge --auto-remove -y python-dev && \
    apt-get autoremove

RUN hg clone -r stable https://www.mercurial-scm.org/repo/evolve/ $KALLITHEA_PATH/evolve/ && \
    cd $KALLITHEA_PATH/evolve/ && \
    echo '[extensions]' >> ~/.hgrc && \
    eval echo 'evolve = $KALLITHEA_PATH/evolve/hgext/evolve.py' >> ~/.hgrc

RUN mkdir -p $KALLITHEA_PATH/conf && \
    mkdir $KALLITHEA_PATH/repos && \
    hg clone https://kallithea.dominikruf.com/kallithea/kallithea-domruf -r docker $KALLITHEA_PATH/src && \
    cd $KALLITHEA_PATH/src && \
    pip install --upgrade -e . && \
#    rm -r $KALLITHEA_PATH/src/.hg && \
    python setup.py compile_catalog

RUN wget https://github.com/jwilder/dockerize/releases/download/v0.2.0/dockerize-linux-amd64-v0.2.0.tar.gz && \
    tar -C /usr/local/bin -xzvf dockerize-linux-amd64-v0.2.0.tar.gz

VOLUME $KALLITHEA_PATH/repos
VOLUME $KALLITHEA_PATH/conf

EXPOSE 5000

WORKDIR $KALLITHEA_PATH/src

ADD kallithea-entry-point.sh $KALLITHEA_PATH/src
RUN chmod +x $KALLITHEA_PATH/src/kallithea-entry-point.sh

ENTRYPOINT ["./kallithea-entry-point.sh"]
CMD ["paster", "serve", "../conf/kallithea.ini"]

