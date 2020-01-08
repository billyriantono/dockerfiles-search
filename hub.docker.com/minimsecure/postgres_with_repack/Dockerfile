FROM postgres:10.5

RUN apt update
RUN apt-get install -y python python-pip postgresql-server-dev-10 libssl-dev libz-dev
RUN pip install -U setuptools
RUN easy_install pgxnclient
RUN rm -rf /usr/bin/pg_config
RUN ln -s /usr/lib/postgresql/10/bin/pg_config /usr/bin/pg_config
RUN pgxn install http://api.pgxn.org/dist/pg_repack/1.4.3/pg_repack-1.4.3.zip
