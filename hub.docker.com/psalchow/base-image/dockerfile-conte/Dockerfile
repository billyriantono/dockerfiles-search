FROM previ/flask

MAINTAINER Roberto Previtera <roberto.previtera@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN pip install python-jose

EXPOSE 5000

RUN mkdir /appl \
    mkdir /appl/api_kvstore

COPY . /appl/api_kvstore

CMD ["python", "/appl/api_kvstore/api.py"]
