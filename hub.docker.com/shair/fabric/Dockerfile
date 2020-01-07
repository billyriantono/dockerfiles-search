FROM python:2.7-stretch

RUN apt-get update && apt-get install -y --no-install-recommends gcc musl-dev libffi-dev make libssl-dev libffi6 openssl openssh-client \
    && pip install fabric==1.14.1 \
    && apt-get remove -y gcc musl-dev libffi-dev make libssl-dev
