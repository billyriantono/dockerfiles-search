FROM python:3

LABEL AUTHOR Toshiyuki Suzumura

WORKDIR /tmp/atrget
RUN apt-get -qq update && \
    apt-get install -y default-jre && \
    pip install html5validator

CMD [ "html5validator", "--root", "/tmp/atrget" ]
