FROM python:3.6.5-slim-stretch

ENV WEB_ROOT /var/gpx/gpx_utils_web

RUN set -x \
    && apt update \
    && apt install -y wget fonts-nanum

RUN set -x \
    && mkdir -p ${WEB_ROOT}

COPY app.py ${WEB_ROOT}/app.py
COPY setup_module.py ${WEB_ROOT}/setup_module.py
    # && wget https://bitbucket.org/whitelazy/gpx_utils_web/get/HEAD.tar.gz \
    # && tar  -C ${WEB_ROOT} -zxf HEAD.tar.gz --strip-components=1 \
    # && rm HEAD.tar.gz \
    # && pip install flask \
RUN set -x \
    && cd ${WEB_ROOT} \
    && python3 setup_module.py

EXPOSE 5000

WORKDIR ${WEB_ROOT}
ENTRYPOINT ["python3", "app.py"]
