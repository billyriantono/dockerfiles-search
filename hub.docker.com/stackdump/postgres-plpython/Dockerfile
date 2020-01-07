FROM postgres:11.1

RUN apt-get update 
RUN apt-get -y install git python3-dev python3-pip python3 postgresql-contrib-11 postgresql-plpython3-11

RUN apt-get clean && \
rm -rf /var/cache/apt/* /var/lib/apt/lists/*

# python package dependencies and db extension
WORKDIR /opt

RUN pip3 install cython>=0.25.1 numpy>=1.14.0
COPY dbapi ./dbapi
COPY requirements.txt .
RUN pip3 install -r ./requirements.txt


# install python db extension
ENV PYTHON_PATH /usr/local/lib/python3.5/dist-packages
ENV PSQL_EDITOR ="/bin/cat"


WORKDIR /docker-entrypoint-initdb.d
RUN echo 'CREATE EXTENSION plpython3u;' > 000_extension.sql

# base state machine tables and functions
COPY ddl/base/ptnet.sql        001_ptnet.sql
COPY ddl/base/pnml.sql         002_pnml.sql
COPY ddl/base/vectors.sql      003_vectors.sql

# python functions
COPY ddl/python/env.sql        101_env.sql
COPY ddl/python/ed25519.sql    102_ed25519.sql
COPY ddl/python/proof.sql      103_proof.sql
COPY ddl/python/harmony.sql    104_harmony.sql

# schemata definitions
COPY ddl/counter/schema.sql    200_counter_schema.sql
COPY ddl/counter/test.sql      201_counter_test.sql

# generate testing data
COPY ddl/python/proof_test.sql 300_proof_test.sql

# examples
COPY examples ./examples

ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 5432
CMD ["postgres"]
