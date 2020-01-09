FROM python:2.7-slim-stretch

LABEL plone=$PLONE_VERSION \
    os="debian" \
    os.version="9" \
    name="Plone 5.1" \
    maintainer="wundertax"

ENV PWD=/plone
ENV XDG_CACHE_HOME=/plone/.cache

RUN useradd --system -U -u 500 plone \
  && mkdir -p /plone/logs /plone/.cache /data

WORKDIR /plone

RUN pip install --no-cache-dir -U setuptools pip virtualenv && virtualenv .

COPY requirements/ /plone/requirements
COPY admin.* /plone/
COPY etc /plone/etc

RUN buildDeps="gcc libc6-dev libpcre3-dev" \
  && runDeps="libmagic-dev gosu" \
  && apt-get update \
  && apt-get install -y --no-install-recommends $buildDeps \
  && ./bin/pip install --no-cache-dir -r /plone/requirements/base_requirements.txt \
  && SUDO_FORCE_REMOVE=yes apt-get purge -y --auto-remove $buildDeps \
  && apt-get install -y --no-install-recommends $runDeps \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

RUN  chmod +x admin.sh \
  && chown -R plone:plone /plone/* /plone/.cache /data

EXPOSE 8080

CMD "/plone/admin.sh"
