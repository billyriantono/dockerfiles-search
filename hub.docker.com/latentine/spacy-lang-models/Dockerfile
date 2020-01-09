FROM python:3.7-alpine

RUN apk update &&\
    apk upgrade &&\
    apk add --no-cache --virtual=build_deps g++ gfortran &&\
    pip install --no-cache-dir spacy &&\
    python -m spacy download en_core_web_sm &&\
    apk del build_deps &&\
    apk add libstdc++