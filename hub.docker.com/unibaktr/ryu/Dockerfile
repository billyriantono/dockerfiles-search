FROM python:alpine
MAINTAINER Marcel Grossmann <whatever4711@gmail.com>
LABEL architecture="amd64"

RUN apk add --update git gcc musl-dev
RUN git clone git://github.com/osrg/ryu.git

RUN sed -i '/BRIDGE_GROUP_ADDRESS/ s/^#*/#/' /ryu/ryu/lib/packet/bpdu.py && \
    sed -i "/BRIDGE_GROUP_ADDRESS/a BRIDGE_GROUP_ADDRESS = '01:80:c2:00:00:0e'" /ryu/ryu/lib/packet/bpdu.py
# Pending PR
COPY bugfixes/ofctl_rest.py /ryu/ryu/app/ofctl_rest.py
COPY bugfixes/wsgi.py /ryu/ryu/app/wsgi.py
COPY bugfixes/stplib.py /ryu/ryu/lib/stplib.py
RUN cd ryu && \
    pip install -r tools/pip-requires && \
    python setup.py install

RUN apk add --update libffi-dev openssl-dev libxml2 libxml2-dev libxslt libxslt-dev && \
    cd /ryu/ryu/app && \
    git clone https://github.com/whatever4711/ryu-starter-kit.git sdnhub_apps && \
    pip install networkx bitarray paramiko eventlet xml_compare pyflakes pylint

WORKDIR ryu

ENV PYTHONPATH=.

ENTRYPOINT ["ryu-manager"]
CMD ["--help"]
