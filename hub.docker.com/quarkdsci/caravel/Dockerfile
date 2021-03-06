FROM ubuntu:14.04
MAINTAINER amancevice@cargometrics.com

# Setup
RUN echo as of 2016-04-03 && \
    apt-get update && \
    apt-get install -y build-essential libssl-dev libffi-dev python-dev python-pip

# Pandas
RUN pip install pandas==0.18.0

# MySQL
RUN apt-get install -y libmysqlclient-dev && pip install mysqlclient==1.3.7

# PostgreSQL
RUN apt-get build-dep -y psycopg2 && pip install psycopg2==2.6.1

# Impala (ref: https://github.com/airbnb/caravel/issues/339)
RUN pip install thrift
RUN pip install six 
RUn pip install bit_array
RUN pip install impyla==0.13.7 

# Caravel
RUN pip install caravel==0.8.9

# Default config
ENV ROW_LIMIT=5000 \
    WEBSERVER_THREADS=8 \
    SECRET_KEY=\2\1thisismyscretkey\1\2\e\y\y\h \
    SQLALCHEMY_DATABASE_URI=sqlite:////home/caravel/caravel.db \
    CSRF_ENABLED=1 \
    DEBUG=1 \
    PYTHONPATH=/home/caravel/caravel_config.py:$PYTHONPATH

EXPOSE 8088

RUN useradd -b /home -m -U caravel
USER caravel

WORKDIR /home/caravel

COPY caravel /home/caravel

CMD ["caravel", "runserver"]
