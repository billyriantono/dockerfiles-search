FROM shippableimages/ubuntu1404_base:latest


# http://bugs.python.org/issue19846
# > At the moment, setting "LANG=C" on a Linux system *fundamentally breaks Python 3*, and that's not OK.
ENV LANG C.UTF-8

RUN add-apt-repository -y ppa:fkrull/deadsnakes;

RUN apt-get update && apt-get install -y \
    python3.3 \
    python3.3-dev \
    python3.4 \
    python3.4-dev;

RUN apt-get install -y \
    postgresql-9.3 \
    postgresql-contrib-9.3 \
    postgresql-server-dev-9.3;

RUN sudo echo "host all all localhost trust" > /etc/postgresql/9.3/main/pg_hba.conf;

RUN sudo echo "local all all trust" >> /etc/postgresql/9.3/main/pg_hba.conf;

RUN sudo service postgresql start;

CMD ["python"]
