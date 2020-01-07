FROM python:2.7

WORKDIR /src
RUN pip install six && \
    curl https://www.zulip.com/dist/api/python-zulip_0.2.5.tar.gz -o python-zulip_0.2.5.tar.gz && \
    tar xf python-zulip_0.2.5.tar.gz && \
    cd zulip-0.2.5 && \
    python setup.py install && \
    rm -rf /src/*
