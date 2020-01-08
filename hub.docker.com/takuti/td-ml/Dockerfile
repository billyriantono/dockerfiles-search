FROM continuumio/miniconda3:latest

WORKDIR /root/

COPY td-client-python /root/td-client-python
COPY td-client-python.patch /root

RUN apt-get update --fix-missing && apt-get -y install gcc g++ libsasl2-dev && \
    conda install -y numpy scipy scikit-learn boto3 sqlalchemy thrift && \
    pip install --upgrade pip && \
    cd td-client-python && \
    patch -p1 < ../td-client-python.patch && \
    pip install . && \
    cd .. && \
    pip install pandas-td pyhive thrift-sasl && \
    pip install git+https://github.com/takuti/PyHivemall.git

CMD ["/bin/sh"]
