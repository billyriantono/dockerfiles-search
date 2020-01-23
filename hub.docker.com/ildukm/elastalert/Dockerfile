FROM python:2.7-alpine

LABEL maintainer="Ildu Kim, https://github.com/ildukim"

ENV ELASTALERT_HOME /opt/elastalert
ENV ELASTALERT_SRC https://github.com/Yelp/elastalert/archive/v0.1.33.zip

WORKDIR /opt

RUN apk update && \
    apk add gcc musl-dev libffi-dev openssl-dev

RUN wget -O elastalert.zip "${ELASTALERT_SRC}" && \
    unzip elastalert.zip && \
    rm elastalert.zip && \
    mv elastalert-* "${ELASTALERT_HOME}"

WORKDIR "${ELASTALERT_HOME}"

RUN pip install "setuptools>=11.3" && \
    python setup.py install

RUN apk del gcc musl-dev libffi-dev openssl-dev

CMD ["python", "-m",  "elastalert.elastalert", "--config",  "/opt/config/config.yaml", "--verbose"]
