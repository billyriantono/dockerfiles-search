FROM python:2

RUN apt-get update && apt-get -y install \
    iproute2 \
    bridge-utils \
    libnetfilter-conntrack-dev \
    libnfnetlink-dev \
    libffi-dev \
    libevent-dev \
    ebtables

WORKDIR /app
COPY broker /app/
RUN python setup.py install

ENTRYPOINT [ "/usr/local/bin/python" ]
CMD [ "-m", "tunneldigger_broker.main", "/tunneldigger.conf" ]
