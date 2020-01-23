FROM fpftech/python-ash-utilities:1.0.0
MAINTAINER André Portela <portela.eng@gmail.com>

ADD requirements.txt /

RUN pip3 install --upgrade pip && \
    pip3 install --no-cache-dir -r /requirements.txt
