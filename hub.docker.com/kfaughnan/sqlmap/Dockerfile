FROM alpine

RUN apk --update --no-cache add \
  git \
  python

RUN mkdir /sqlmap /work && \
  git clone --depth 1 https://github.com/sqlmapproject/sqlmap.git /sqlmap

RUN apk del \
  git

VOLUME ["/work"]

WORKDIR /work

ENTRYPOINT ["python","/sqlmap/sqlmap.py"]
