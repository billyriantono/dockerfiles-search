FROM python:2-alpine as build
RUN apk add --update libffi-dev
RUN apk add --update openssl-dev
RUN apk add --update build-base
ADD ./setup.py /install/setup.py
ADD ./cassandra_snapshotter /install/cassandra_snapshotter
WORKDIR /install
RUN pip install .

FROM python:2-alpine
RUN apk add --update libffi-dev
RUN apk add --update openssl-dev
RUN apk add --update lzo
ENTRYPOINT ["cassandra-snapshotter"]
COPY --from=build /usr/local/lib/python2.7/site-packages /usr/local/lib/python2.7/site-packages
COPY --from=build /usr/local/bin/cassandra-snapshotter /usr/local/bin/cassandra-snapshotter
