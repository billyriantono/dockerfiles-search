FROM python:2.7.15-alpine3.9

ARG version=1.7.1

WORKDIR /app

RUN wget https://github.com/harelba/q/archive/${version}.tar.gz && \
  tar zxf ${version}.tar.gz && \
  ln -s /app/q-${version}/bin/q /usr/local/bin/q

ENTRYPOINT ["q"]
CMD [""]
