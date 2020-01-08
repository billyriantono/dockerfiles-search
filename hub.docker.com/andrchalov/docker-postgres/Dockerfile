
FROM postgres:10.10

ENV \
	PGTAP_VERSION=0.99.0 \
  URL_ENCODE_VERSION=1.2.3

RUN set -x \
  && apt-get update \
  && apt-get install -y --no-install-recommends \
      ca-certificates \
      build-essential \
      wget \
      openssl \
      postgresql-server-dev-10 \
      postgresql-plpython-10 \
      python-pip \
      python-setuptools

# Install pgtap
RUN set -x \
  && wget https://github.com/theory/pgtap/archive/v${PGTAP_VERSION}.tar.gz \
  && tar -xzvf v${PGTAP_VERSION}.tar.gz \
  && rm -f v${PGTAP_VERSION}.tar.gz \
  && cd pgtap-${PGTAP_VERSION} \
  && make \
  && make install \
  && cd .. \
  && rm -rf pgtap-${PGTAP_VERSION}

# Install url_encode
RUN set -x \
  && wget https://github.com/okbob/url_encode/archive/v${URL_ENCODE_VERSION}.tar.gz \
  && tar -xzf v${URL_ENCODE_VERSION}.tar.gz \
  && cd url_encode-${URL_ENCODE_VERSION} \
  && make \
  && make install \
  && cd .. \
  && rm -Rdf url_encode-${URL_ENCODE_VERSION} v${URL_ENCODE_VERSION}.tar.gz

# install python modules
RUN set -x \
	&& pip install -t /usr/lib/python2.7 requests \
	&& pip install -t /usr/lib/python2.7 pyyaml \
	&& pip install -t /usr/lib/python2.7 requests_toolbelt

RUN set -ex \
  && apt-get -y remove python-setuptools \
  && apt-get purge -y --auto-remove wget build-essential \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*;

COPY docker-entrypoint.sh /
RUN chmod 755 /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 5432

CMD ["postgres"]
