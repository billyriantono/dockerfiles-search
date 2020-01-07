FROM postgres:9.6
RUN apt-get update && apt-get install -y git python python-pip python-dev wget unzip python-psycopg2 python-numpy libyaml-dev libpq-dev postgresql-server-dev-9.6 && rm -rf /var/lib/apt/lists/*
RUN cd /tmp && wget http://api.pgxn.org/dist/multicorn/1.3.3/multicorn-1.3.3.zip && unzip multicorn-1.3.3.zip && cd multicorn-1.3.3/ && make && make install
