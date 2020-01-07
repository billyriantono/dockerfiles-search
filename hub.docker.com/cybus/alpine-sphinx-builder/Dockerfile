FROM frolvlad/alpine-python3

RUN apk add --update make && \
    pip3 install sphinx sphinxcontrib-swaggerdoc

ENTRYPOINT make html