FROM python:3-alpine
RUN apk add --no-cache libpq && \
    apk add --no-cache --virtual build-dep git postgresql-dev gcc musl-dev && \
    git clone https://github.com/perseas/Pyrseas.git && \
    cd Pyrseas && \
    python setup.py build && \
    python setup.py install && \
    cd .. && \
    rm -r Pyrseas && \
    apk del build-dep
