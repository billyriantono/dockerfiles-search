FROM python:2.7

MAINTAINER Bear <bear@blbear.com>

ADD . /code
WORKDIR /code

RUN pip install -r requirements.txt

ADD . /protos
ADD . /out

COPY protoc-gen-lua/* /usr/local/bin/

COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh
RUN chmod +x /usr/local/bin/docker-entrypoint.sh

ENTRYPOINT ["docker-entrypoint.sh"]
CMD [""]