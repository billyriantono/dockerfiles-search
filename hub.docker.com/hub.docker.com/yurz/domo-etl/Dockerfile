FROM yurz/pybase:latest

LABEL authors="Yuri Zhylyuk yuri@zhylyuk.com"

RUN \
    apt-get -y update \
    && apt-get -y install git \
    && conda update conda \
    && conda install -y -c conda-forge pip pandas \
        requests lxml pytz xlrd SQLAlchemy psycopg2 pymssql mysql \
    && pip install --upgrade \
        git+https://github.com/domoinc/domo-python-sdk.git \
    && conda clean -y -a \
    && apt-get clean autoclean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/{cache,log}/ \
    mkdir /app
WORKDIR /app
CMD ["python", "./app.py"]